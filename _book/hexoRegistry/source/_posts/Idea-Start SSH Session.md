# ssh连接服务器

- Tools => Start SSH Session => Edit credentials...
- 输入host、port、name和密码，点击ok即可出现连接后的控制台。(这里不能保存会话信息，每次连接都要重新输入一遍)



# 保存会话信息

- Tools => Deployment => Configuration
- 点击左上角的 + 号 
  - 设置name为测试
  - type选择 SFTP
- 然后开始输入host、port、name和密码，可以点击 Test SFTP connection测试连接
- 点击save password，最后点击ok即可
- 这样Tools => Start SSH Session => 就会出现刚才命名的会话测试

