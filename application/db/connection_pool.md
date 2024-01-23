# DB Connection pool

```mermaid
flowchart LR
  APP[Application]
  subgraph ConnectionPool
    C1[Connection]
    C2[Connection]
    C3[Connection]
    C4[Connection]
  end
  DB[(Database)]
  APP --> ConnectionPool
  ConnectionPool --> DB
  DB --> C1
  DB --> C2
  DB --> C3
  DB --> C4
```
