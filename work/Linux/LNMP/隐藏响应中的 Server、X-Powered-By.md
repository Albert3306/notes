# 隐藏响应中的 Server、X-Powered-By

```Linux
# 隐藏X-Powered-By
# 修改 php.ini 文件 设置 expose_php = Off

# apache 隐藏 server
# 修改httpd.conf 设置 
ServerSignature Off
ServerTokens Prod

# nginx 隐藏 server
# 修改nginx.conf  在http里面设置 
server_tokens off;
```

