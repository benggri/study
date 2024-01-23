# DB Connection pool

```
 --------------------------------------                              ----------  
| Application Server                   | -- request connections --> | Database | 
 --------------------------------------                              ----------  
|  -------------    -----------------  |                                 |       
| | Application |  | Connection pool | |                                 |       
|  -------------    -----------------  |                                 |       
|                  |     connection  | | <-------------------------------|       
|                  |     connection  | | <-------------------------------|       
|                  |     connection  | | <-------------------------------|       
|                  |     connection  | | <-------------------------------        
|                   -----------------  |                                         
 --------------------------------------                                         
```

- Application Server 에서 Connection pool 을 만든다
- Application Server 에서 Database 에 Connection 요청을 한다
- Application 은 Connection pool 에 연결된 connection 을 이용하고 반환한다
- Connection pool 을 사용한면 Database connection 수를 제한할 수 있어서 과도한 접속으로 인한 서버 자원 고갈을 방지할 수 있다
