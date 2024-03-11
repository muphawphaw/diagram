```mermaid

flowchart LR
    A(Web)
    B(Mobile)
 
    A & B-->|request api|J[Load balancer]
    J-->|api call|C((Api Gateway))
    
    subgraph Microservices
    C-->|sent request|D[service 1]
    C-->|sent request|E[service 2]
    C-->|sent request|F[service 3]
    D-->G[(Database 1)]
    E-->H[(Database 2)]
    F-->I[(Database 3)]
    end
    G & H & I --> K[Response]