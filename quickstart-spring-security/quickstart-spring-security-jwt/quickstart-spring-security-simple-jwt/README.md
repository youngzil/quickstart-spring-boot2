
参考 [SpringBoot Security整合JWT授权RestAPI](https://segmentfault.com/a/1190000021127877)  
[代码](https://github.com/qianmoQ/spring-learn-integration/tree/master/security/security-jwt)



#### 校验授权

---

- 在控制台输入以下命令(**未授权时**)

```bash
curl -X GET 'http://localhost:8989/auth/hello'
```

会出现以下错误信息

```bash
{
    "timestamp": "2019-11-26T13:05:05.204+0000",
    "status": 403,
    "error": "Forbidden",
    "message": "Access Denied",
    "path": "/auth/hello"
}
```

- 提示我们未授权,这时我们使用`/auth/login`去获得授权的token

```bash
curl -X POST 'http://127.0.0.1:8989/auth/login' --header 'Content-Type: application/json' -d '{"username": "admin", "password": "password"}'
```

返回以下token信息

```bash
eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTYxODQ5NDAwOH0.Hl6ZZwz0OSxeNF2xb-JDjLSkLFl0isS9jFqqa2enMCqfiPc2c-0zbpXVLp-JUa6z0QOSmiEnc5MftVsBAoHLEQ
```

- 这时我们使用返回的token进行访问`/auth/hello`接口获取数据

```bash
curl -X GET 'http://127.0.0.1:8989/auth/hello' --header 'Authorization: eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTYxODQ5NDAwOH0.Hl6ZZwz0OSxeNF2xb-JDjLSkLFl0isS9jFqqa2enMCqfiPc2c-0zbpXVLp-JUa6z0QOSmiEnc5MftVsBAoHLEQ'
```

返回以下信息

```bash
Hello Jwt!!!
```

此时我们已经完成JWT授权配置