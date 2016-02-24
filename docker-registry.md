
#启动registry，并且添加验证
- 生成auth的账户和密码
  `htpasswd -nbB <username> <password> > htpasswd`
- 将htpasswd放到/auth/htpasswd
- 将证书chained.pem和私钥domain.key放到/certs里面
```
docker run -d -p 443:5000 --restart=always -v /certs:/certs -v /root/auth:/auth -v /registry:/var/lib/registry -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/chained.pem -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key --name registry registry:2
```
