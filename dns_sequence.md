```mermaid 
sequenceDiagram
    Web Browser->>+Browser cache:check the IP address
    alt Yes
    Browser cache->>-Web Browser : Sent IP address
    else No
    Browser cache->>+Operating System cache: check IP adderss
    end
    Operating System cache->>-Web Browser: Sent IP address
    Operating System cache->>+ISP cache: check IP address
    alt Yes 
    ISP cache->>-Web Browser: Sent IP address
    else No
    ISP cache->>Reslover: request IP address
    end