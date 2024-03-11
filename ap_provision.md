```mermaid
flowchart TD
subgraph One
    A((Start))-->B[Get UUID]
    B-->C[Check cable connection]
    C-->D{Connected == ?}
    D-->|Yes|E[Check AP is alive]
    D-->|NO|F[Wait]
    
    
    E-->G{AP Alive == ?}
    G-->|No|H[Wait]
    G-->|Yes|I[Get MAC]
     end 

subgraph Two
    J[Use IP]
    J-->K[Establish SSH connection\n to the device]
    K-->|connected to the device|L[Get hardware \n information]
    L-->M[Get model]
    M-->|request api|N[Get Model requirements]
end

subgraph Three
    O[Use MAC]-->|call api|P[Check device profile]
    P-->Q{MAC in Device profile == ??}
    %% if YES
    Q-->|YES|W[Reprovision]
    W-->R[Factory Reset]

     %% If NO
    Q-->|NO|X[Provision]
    X-->|request api|Y[Create New profile]


    R & Y -->Z[Get Data]
    Z -->S[Update script and configs]
    S-->T[Reboot the device and \n wait till it is up again]
    T-->U[Establish SSH connection \nwith provision IP]
    U-->|connected to the device|V[Set a unique password\n for the device]

   
  end
  I-->Two
  N-->Three