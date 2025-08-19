# Github .md mermaid

```mermaid
flowchart LR
    subgraph k8s[Kubernetes]
        direction LR
        subgraph fe[Frontend]
            direction LR
            fe-svc("fab:fa-youtube")
        end
    end

    style fe stroke-width:2px,stroke-dasharray: 5 5
```
