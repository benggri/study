# Architecture

- Frontend, BFF(Backend For Frontend), Backend, Batch, Database로 구성된 예시입니다.
- Frontend와 BFF(Backend For Frontend)는 1:1로 호출하게 됩니다.
- Backend와 Database는 1:1로 연결됩니다.
- Batch와 Database는 1:1로 연결됩니다.
- BFF(Backend For Frontend)는 여러 Backend와 호출할 수 있어야 합니다.

```mermaid
flowchart LR
    subgraph MSA ["Micro Services"]
        direction LR
        subgraph K8S-1 ["Kubernetes"]
            direction LR
            subgraph FE-1 ["Frontend"]
                fe-1@{ shape: processes, label: "Next.js" }
            end
            subgraph BFF-1 ["BFF"]
                bff-1@{ shape: processes, label: "Nest.js" }
            end
            subgraph BE-1 ["Backend"]
                direction LR
                be-rest-1@{ shape: processes, label: "Springboot(RestAPI)" }
                be-grpc-1@{ shape: processes, label: "Nest.js(gRPC)" }
            end
            subgraph BT-1 ["Batch"]
                direction LR
                bt-1@{ shape: processes, label: "Springboot(Batch)" }
            end
        end
        FE-1 --- BFF-1 --- BE-1 ~~~ BT-1

        subgraph K8S-2 ["Kubernetes"]
            direction LR
            subgraph FE-2 ["Frontend"]
                fe-2@{ shape: processes, label: "Next.js" }
            end
            subgraph BFF-2 ["BFF"]
                bff-2@{ shape: processes, label: "Nest.js" }
            end
            subgraph BE-2 ["Backend"]
                direction LR
                be-rest-2@{ shape: processes, label: "Springboot(RestAPI)" }
                be-grpc-2@{ shape: processes, label: "Nest.js(gRPC)" }
            end
            subgraph BT-2 ["Batch"]
                direction LR
                bt-2@{ shape: processes, label: "Springboot(Batch)" }
            end
        end
        FE-2 --- BFF-2 --- BE-2 ~~~ BT-2

        subgraph K8S-3 ["Kubernetes"]
            direction LR
            subgraph FE-3 ["Frontend"]
                fe-3@{ shape: processes, label: "Next.js" }
            end
            subgraph BFF-3 ["BFF"]
                bff-3@{ shape: processes, label: "Nest.js" }
            end
            subgraph BE-3 ["Backend"]
                direction LR
                be-rest-3@{ shape: processes, label: "Springboot(RestAPI)" }
                be-grpc-3@{ shape: processes, label: "Nest.js(gRPC)" }
            end
            subgraph BT-3 ["Batch"]
                direction LR
                bt-3@{ shape: processes, label: "Springboot(Batch)" }
            end
        end
        FE-3 --- BFF-3 --- BE-3 ~~~ BT-3
    end

    subgraph MSA-DB ["MSA Databases"]
      subgraph DB ["Database"]
        db-1[("PostgreSQL")]
      end
      subgraph DB-2 ["Database"]
        db-2[("MongoDB")]
      end
      subgraph DB-3 ["Database"]
        db-3[("PostgreSQL")]
      end
    end

    BFF-1 --- BE-2
    BFF-1 --- BE-3
    BFF-2 --- BE-1
    BFF-2 --- BE-3
    BFF-3 --- BE-1
    BFF-3 --- BE-2
    BE-1 --- db-1
    BE-2 --- db-2
    BE-3 --- db-3
    BT-1 <--> db-1
    BT-2 <--> db-2
    BT-3 <--> db-3
```
