在cas-overlay基础上, 根据文档配置的支持oauth 2.0协议的服务端。
cas文档：http://jasig.github.io/cas/4.0.x/index.html
cas构建基础：https://github.com/github/cas-overlay
构建命令：mvn clean package 将生成的war包，放到/var/lib/tomcat7/webapps/下， 重启tomcat。
访问https://localhost:8443/cas即可。

目前oauth_consumer_key和oauth_consumer_secret硬编码在配置文件中，项目启动时载入到内存中。
实际项目中，需要从数据库或json文件中读取。
APP ID：477037
API KEY：9ad1c51571f9479d8f5df19e5f63f07c
Secret Key：2bf4a68d6d0147feadb9fbeaf582b561

可以在浏览器输入如下ＵＲＬ测试该服务端是否正常。
https://localhost:8443/cas/oauth2.0/authorize?client_id=9ad1c51571f9479d8f5df19e5f63f07c&redirect_uri=http://www.syberos.com/&response_type=code
此处client_id即为上述的API KEY。该url执行完毕，将返回ＳＴ。

https://localhost:8443/cas/oauth2.0/accessToken?client_id=9ad1c51571f9479d8f5df19e5f63f07c&client_secret=2bf4a68d6d0147feadb9fbeaf582b561&redirect_uri=http://www.syberos.com/&code=ST-1-RbxAfWfqjrhcsbe0e017-casauth
此处client_id即为上述的API KEY；client_secret即为上述的Secret Key；code即为上面生成的ＳＴ。根据实际生成值修改。该url执行完毕，将返回ＴＧＴ。

https://localhost:8443/cas/oauth2.0/profile?access_token=TGT-1-pRLlFefgqIhtDvMl6L162LRsqlxylv3ogwTwcH6DRp4LYcadE2-cas01.example.org
此处access_token即为上述的ＴＧＴ。


后端使用ldap存储用户信息。修改cas.properties相应的字段，正确配置ldap信息。
