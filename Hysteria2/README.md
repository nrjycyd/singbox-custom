# **installation**

- ## **Download the precompiled version of sing-box**
- AMD core
```
wget -c "https://github.com/SagerNet/sing-box/releases/download/v1.5.0-beta.2/sing-box-1.5.0-beta.2-linux-amd64.tar.gz" -O - | tar -xz -C /usr/local/bin --strip-components=1 && chmod +x /usr/local/bin/sing-box
```
- ARM core
```
wget -c "https://github.com/SagerNet/sing-box/releases/download/v1.5.0-beta.2/sing-box-1.5.0-beta.2-linux-arm64.tar.gz" -O - | tar -xz -C /usr/local/bin --strip-components=1 && chmod +x /usr/local/bin/sing-box
```
- ## **Configure the systemd service of sing-box**
```
wget -P /etc/systemd/system https://raw.githubusercontent.com/TinrLin/Install_sing-box/main/Hysteria2/sing-box.service
```
- ## **Download and modify the sing-box configuration file**
```
mkdir /usr/local/etc/sing-box && wget -P /usr/local/etc/sing-box https://raw.githubusercontent.com/TinrLin/Install_sing-box/main/Hysteria2/congfig.json
```
- ## **Start and run sing-box**
```
systemctl daemon-reload && systemctl enable --now sing-box && systemctl status sing-box
```

