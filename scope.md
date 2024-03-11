```mermaid
    flowchart LR
    A((Consumer))-->B[Check Event Type]
    B-->C{Event type committed ==?}

    %%check event type (No)

    C-->|No|D[End Session]

    %%check event type (Yes)

    C-->|Yes|E[Check hash value]
    E-->F{same hash == ?}

    %% check hash value
    F-->|True|G[Skip]
    F-->|False|I[Check Client]
    I-->J{New Client == ?}

    %%check client
    J-.->|Yes|K[Invalidate old session and open new one]
    J-.-|No|L[Start Session]
    L-.->M[Get option60]
    K-.->M

    %%check option60
    M-->N{Option60 ?}
    N-.->|Yes|O[Get CID]
    N-.->|No|P[Use MAC to get CID]
    P-.->O
    
    %% api call
    O-->|api call|Q[Bandwidth]
    Q-->|api call|R[Service Type]
    R-->S[Sent the data]
    S-->T[Binder]