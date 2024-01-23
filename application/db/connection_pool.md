# DB Connection pool

```
 -----------------------                              ----------  
| Application Server    | -- request connections --> | Database | 
 -----------------------                              ----------  
|     Connection pool   |                                 |       
|         connection    | <-------------------------------|       
|         connection    | <-------------------------------|       
|         connection    | <-------------------------------|       
|         connection    | <-------------------------------        
 -----------------------                                         
```

- Application 에서 Database 에 Connection 요청을 한다
- 
