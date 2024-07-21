

## **安装sing-box**
#### **更新软件源及安装依赖**
```
apt update && apt -y install wget tar socat curl
```

#### **官方脚本安装**
- **地址：**[包管理器 - sing-box (sagernet.org)](https://sing-box.sagernet.org/zh/installation/package-manager/)
```
bash <(curl -fsSL https://sing-box.app/deb-install.sh)
```

> [!IMPORTANT]
> **官方脚本安装文件路径**  
> 内核文件：`/usr/bin/sing-box`  
> systemd 服务文件：`/usr/lib/systemd/system/sing-box.service`  
> config 配置文件：`/etc/sing-box/config.json`

#### **下载预发布版sing-box**
- **预编译版下载地址：** https://github.com/SagerNet/sing-box/releases.
- **AMD 内核**
```
wget -c "https://github.com/SagerNet/sing-box/releases/download/v1.5.0-beta.2/sing-box-1.5.0-beta.2-linux-amd64.tar.gz" -O - | tar -xz -C /usr/local/bin --strip-components=1 && chmod +x /usr/local/bin/sing-box
```
## **配置 sing-box 的 systemd 服务**
```
wget -P /etc/systemd/system https://raw.githubusercontent.com/nrjycyd/singbox-custom/main/Hysteria2/sing-box.service
```


## **配置 sing-box 的config文件**
- **下载并修改config文件**

```
mkdir /usr/local/etc/sing-box && wget -P /usr/local/etc/sing-box https://raw.githubusercontent.com/nrjycyd/singbox-custom/main/Hysteria2/self-signed_config.json
```

- **重命名config文件**

```
mv /usr/local/etc/sing-box/self-signed_config.json /usr/local/etc/sing-box/config.json
```
## **配置证书**

- **创建安装目录**
```
mkdir -p /etc/ssl/self-signed
```
- **生成私钥，安装到指定目录**

```
openssl ecparam -genkey -name prime256v1 -out /etc/ssl/self-signed/private.key
```

- **生成证书，安装到指定目录**

```
openssl req -new -x509 -days 3650 -key /etc/ssl/self-signed/private.key -out /etc/ssl/self-signed/cert.crt -subj "/CN=bing.com"
```

## **Hysteria端口跳跃**

```
# Debian&&Ubuntu

## 安装iptables-persistent
apt install iptables-persistent

## 清空默认规则
iptables -F

## 清空自定义规则
iptables -X

## 允许本地访问
iptables -A INPUT -i lo -j ACCEPT

## 开放SSH端口（假设SSH端口为22）
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

## 开放HTTP端口
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

## 开放UDP端口（10860替换为节点的监听端口）
iptables -A INPUT -p udp --dport 10860 -j ACCEPT

## 开放UDP端口范围（假设UDP端口范围为30000-50000）
iptables -A INPUT -p udp --dport 30000:50000 -j ACCEPT

## 允许接受本机请求之后的返回数据
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

## 其他入站一律禁止
iptables -P INPUT DROP

## 允许所有出站
iptables -P OUTPUT ACCEPT

## 查看开放的端口
iptables -L

## 添加NAT规则，30000:50000替换为你设置端口跳跃的范围，10860替换为你节点的监听端口
iptables -t nat -A PREROUTING -p udp --dport 30000:50000 -j DNAT --to-destination :10860

## 查看NAT规则
iptables -t nat -nL --line

## 保存iptables规则
netfilter-persistent save
```
## **启动并运行sing-box**
- **验证config.json格式：** https://jsonlint.com/
- **检查sing-box配置**
```
/usr/local/bin/sing-box run -c /usr/local/etc/sing-box/config.json
```

> [!IMPORTANT]
> **官方脚本配置 检查sing-box**  
> `/usr/bin/sing-box run -c /etc/sing-box/config.json`


- **启动并运行sing-box**
```
systemctl daemon-reload && systemctl enable --now sing-box && systemctl status sing-box
```
- **sing-box其他指令**
```
systemctl start sing-box    #启动
systemctl stop sing-box    #停止
systemctl restart sing-box    #重启
systemctl status sing-box    #查看状态
...
sing-box generate uuid    #生成UUID
sing-box generate reality-keypair    #生成private_key
...
```

