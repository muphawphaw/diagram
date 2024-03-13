```mermaid
sequenceDiagram
    par Me to Mom
        Me->>Mom: Can I borrow some money?
    and Me to Dad
        Me->>Dad: Can I borrow some money?
    end
    Mom-->>Me: Give Money
    Dad-->>Me: No money
    par Me to village
        Me->>Village : Go to Village
    and Me to Merchant
        Me->>Merchant : Buy pigs
    end
    Merchant-->>Me : Give pigs
    Me->>Merchant : Sell pigs