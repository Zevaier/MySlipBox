# Title

配置个人服务器的ssh服务

---

# Keywords

ssh

---
# Content

## Requirement
在个人服务器上配置ssh服务，便于远程控制服务器。
+ 便利性。直接使用root用户登陆，无需从其他用户登陆切换root用户。
+ 安全性。仅允许密钥登陆，不允许密码登陆。
+ 其他。修改默认端口。

## Process

1. 修改ssh服务配置文件，重启ssh服务。
```shell
> sed -i 's/^port\|^PermitRootLogin\|PasswordAuthentication/#&/g' /etc/ssh/sshd_config
> echo 'port 10022' >> /etc/ssh/sshd_config
> echo 'PermitRootLogin prohibit-password' >> /etc/ssh/sshd_config
> echo 'PasswordAuthentication no' >> /etc/ssh/sshd_config
> service sshd restart
```
相关ssh服务配置说明：
- port ：ssh服务端口；
- PermitRootLogin：root登录选项： `no`（默认，不允许root远程登录），`yes`（允许root远程登录）, `prohibit-password`（禁止root远程密码登录）；
- PasswordAuthentication：密码授权选项：`yes`（默认，允许），`no`（禁止）。


2. 关闭selinux。selinux会导致阻止ssh服务在10022端口启动。
```shell
> sed -i 's/\(SELINUX=\).*/\1disabled/' /etc/selinux/config
> reboot 0
```



3. 生成root的密钥。
```shell
> ssh-keygen -t rsa
Enter file in which to save the key (/root/.ssh/id_rsa): root@myserver.rsa
> mv ./root@myserver.rsa.pub /root/.ssh/authorized_keys
> chmod 700 /root
> chmod 700 /root/.ssh
> chmod 600 /root/.ssh/authorized_keys
> chown root /root/.ssh/authorized_keys
```
相关说明：
- `ssh-keygen -t rsa`生成rsa私钥文件和对应的公钥文件。
- ssh配置默认用户的登陆公钥需要放在用户目录下的.ssh/authorized_keys文件中。
- ssh对公钥文件及其目录访问权限有严格限制。

4. 客户机登录。
```shell
> ssh root@<server_ip> -p 10022 -i <private_key_file_name>
```

<p align="right">2022.07.03</p>

---
# References

无。

---
# Links

无。


