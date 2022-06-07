# 轻量级服务器配置流程

## 删除阿里云云盾
```bash
wget -qO- https://raw.githubusercontent.com/DGideas/config/master/uninstall_aliyun.sh | bash
```
## 更新内核
```bash
do-release-upgrade
```
## apt 4连
```bash
apt-get update && apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get clean
```
### 或者
```bash
apt-get update
```
```bash
apt-get dist-upgrade -y
```
apt-get autoremove --purge -y
apt-get clean
```
## 新系统一键BBR
```bash
wget -qO- https://raw.githubusercontent.com/DGideas/config/master/one_key_bbr.sh | bash
```
## 安装Anyconnect
```bash
apt-get install ocserv
```
## 申请SSL证书
```bash
apt-get install apache2
apt-get install snapd
snap install core
snap refresh core
apt-get remove certbot
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot
certbot --apache
certbot renew --dry-run
certbot certonly
```
## 改ocserv 443 端口
```bash
systemctl status ocserv.socket
(Unit ocserv.socket could not be found.)
```
## 查看系统中哪个端口被占用
```bash
netstat -unltp
```
## 改ocserv的配置
/etc/ocserv/ocserv.conf
把准备好的文件复制上去
```bash
ocpasswd -c /etc/ocserv/ocpasswd qiuguanglei
ocserv -c /etc/ocserv/ocserv.conf
netstat -tulpn | grep 443
```
## 打开系统的转发功能
/etc/sysctl.conf
把准备好的文件复制上去
```bash
sysctl -p
```
## 开启NAT
```bash
iptables -t nat -A POSTROUTING -j MASQUERADE
```