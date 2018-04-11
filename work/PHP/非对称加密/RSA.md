# 非对称加密之 RSA

[TOC]



## 1、生成证书和获取公钥、私钥

- ### Windows 环境

```
# 开启 PHP php_openssl 扩展

# 生成证书
$configargs = [ // 获取 openssl.cnf 绝对地址
    'config' => 'E:\wamp64\bin\apache\apache2.4.23\conf\openssl.cnf'
];
$resource = openssl_pkey_new($configargs);

# 获取私钥
openssl_pkey_export($resource, $private_key, null, $configargs);

# 获取公钥
$detail = openssl_pkey_get_details($resource);
$public_key = $detail['key'];
```

- ### Linux 环境

```
# 生成私钥
openssl genrsa -out rsa_private_key.pem

# 生成公钥
openssl rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
```

## 2、加密和解密

```
# 公钥加密
openssl_public_encrypt($data, $encrypted, $public_key);
base64_encode($encrypted);

# 公钥解密
openssl_public_decrypt(base64_decode($data), $decrypted, $public_key);

# 私钥加密
openssl_private_encrypt($data, $encrypted, $private_key);
base64_encode($encrypted);

# 私钥解密
openssl_private_decrypt(base64_decode($data), $decrypted, $private_key);
```

