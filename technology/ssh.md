# Title

配置ssh服务

---

# Keywords

ssh

---
# Content

1. 修改sshd服务配置文件，设置端口为10022，允许远程密钥登陆，禁止远程密码登录。
```shell
echo 'port 10022' >> /etc/ssh/sshd_config
echo 'PermitRootLogin prohibit-password' >> /etc/ssh/sshd_config
echo 'PasswordAuthentication no' >> /etc/ssh/sshd_config
```

2. 关闭selinux
```shell
sed -i 's/\(SELINUX=\)[a-z]*/\1disabled/' /etc/selinux/config
reboot 0
```

3. 启动sshd，生成root的密钥
```shell
service sshd restart
midkr /root/.ssh/authorized_keys
chmod 700 /root
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
chown root /root/.ssh/authorized_keys
ssh-keygen -t rsa
```
<p align="right">2022.06.12</p>

---
# References

(文中提及的参考文献)  
[1] 2022, zhan..., "模板规范", 出版社名.

---
# Links

(相关的笔记链接)  
[1] [这是本篇的标题](./template.md)


