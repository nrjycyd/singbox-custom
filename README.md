## To check the system's kernel architecture, you can use the uname command with the -m option.
```
uname -m
```
- **amd64(x86_64、x64): Indicates the 64-bit kernel.**
- **386(i686 or i386): Indicates a 32-bit kernel.**
- **armv7l: Indicates a 32-bit ARM-based kernel.**
- **arm64(aarch64): Indicates a 64-bit ARM-based kernel.**
## The download URL for Go is [https://golang.org/dl/](https://go.dev/dl/).
```
wget -c https://go.dev/dl/go1.20.5.linux-amd64.tar.gz -O - | tar -xz -C /usr/local && echo 'export PATH=$PATH:/usr/local/go/bin' > /etc/profile && source /etc/profile && go version
```
- **'wget': This command is used to download files from the internet.**
- **'-c': This option tells 'wget' to continue a previously interrupted download if the file already exists, allowing you to resume the download from where it left off.**
- **'https://go.dev/dl/go1.20.5.linux-amd64.tar.gz': This is the URL of the Go language archive file for the Linux AMD64 architecture. It is the file that will be downloaded using 'wget'.**
- **'-O -': This option tells 'wget' to output the downloaded file to the standard output (stdout) instead of saving it to a file on disk. The hyphen "-" means stdout.**
- **'|': This is a pipe symbol, used to redirect the standard output of one command to the standard input of another command.**
- **'tar -xz -C /usr/local': This part of the command uses 'tar' to extract the downloaded archive file (Go language) from the standard input (piped from 'wget') and extract its contents into the '/usr/local' directory.**
- **'PATH=$PATH:/usr/local/go/bin': Setting the PATH environment variable.**
- **The command 'source /etc/profile' is used to load and apply the changes made to the global system environment variables and settings defined in the '/etc/profile' file.**
- **The command 'go version' is used to check the installed version of the Go programming language on your system.**
## Install sing-box with option
```
go install -v -tags \
with_quic,\              
with_grpc,\             
with_dhcp,\            
with_wireguard,\         
with_shadowsocksr,\     
with_ech,\              
with_utls,\             
with_reality_server,\    
with_acme,\              
with_clash_api,\         
with_v2ray_api,\        
with_gvisor,\           
with_embedded_tor,\     
with_lwip \            
github.com/sagernet/sing-box/cmd/sing-box@latest
```
- **'with_quic' Build with QUIC support, see QUIC and HTTP3 DNS transports, Naive inbound, Hysteria Inbound, Hysteria Outbound and V2Ray Transport#QUIC.**
- **'with_grpc' Build with standard gRPC support, see V2Ray Transport#gRPC.**
- **'with_dhcp' Build with DHCP support, see DHCP DNS transport.**
- **'with_wireguard' Build with WireGuard support, see WireGuard outbound.**
- **'with_shadowsocksr' Build with ShadowsocksR support, see ShadowsocksR outbound.**
- **'with_ech' Build with TLS ECH extension support for TLS outbound, see TLS.**
- **'with_utls' Build with uTLS support for TLS outbound, see TLS.**
- **'with_reality_server' Build with reality TLS server support, see TLS.**
- **'with_acme' Build with ACME TLS certificate issuer support, see TLS.**
- **'with_clash_api' Build with Clash API support, see Experimental.**
- **'with_v2ray_api' Build with V2Ray API support, see Experimental.**
- **'with_gvisor' Build with gVisor support, see Tun inbound and WireGuard outbound.**
- **'with_embedded_tor' Build with embedded Tor support, see Tor outbound.**
- **'with_lwip' Build with LWIP Tun stack support, see Tun inbound.**
## Install sing-box using the precompiled version(supports some functions)
### The download URL for sing-box is [https://github.com/SagerNet/sing-box/releases](https://github.com/SagerNet/sing-box/releases).
```
wget -c "https://github.com/SagerNet/sing-box/releases/download/v1.3.6/sing-box-1.3.6-linux-amd64.tar.gz" -O - | tar -xz -C /usr/local/bin --strip-components=1 && chmod +x /usr/local/bin/sing-box
```
- **'wget -c "https://github.com/SagerNet/sing-box/releases/download/v1.3.6/sing-box-1.3.6-linux-amd64.tar.gz"': This part of the command uses the 'wget' utility to download the Sing-Box release version 1.3.6 for Linux (64-bit) from the specified URL. The '-c' option is used to continue the download if it's interrupted or if a partially downloaded file exists.**
- **'-O -': This part of the command tells 'wget' to output the downloaded content to the standard output (stdout) instead of saving it to a file.**
- **'|': The pipe symbol pipes the output of the first command ('wget') as input to the second command ('tar').**
- **'tar -xz -C /usr/local/bin --strip-components=1': This part of the command uses the 'tar' utility to extract the contents of the downloaded tar.gz archive. The options '-x' and '-z' tell 'tar' to extract and decompress the gzip-compressed archive. The '-C /usr/local/bin' option specifies the target directory where the extracted files will be placed, in this case, '/usr/local/bin'. The '--strip-components=1' option tells 'tar' to remove the top-level directory when extracting, so the files are directly placed in '/usr/local/bin' without the unnecessary directory level.**
- **'&&': The double ampersand is a shell operator used to execute the next command only if the previous command succeeds (exits with a status of 0).**
- **'chmod +x /usr/local/bin/sing-box': This part of the command sets the executable (+x) permission on the 'sing-box' binary located in '/usr/local/bin', making it executable.**
## systemd service unit file for sing-box service
```
[Unit]
Description=sing-box service
Documentation=https://sing-box.sagernet.org
After=network.target nss-lookup.target

[Service]
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
ExecStart=/usr/local/bin/sing-box run -c /usr/local/etc/sing-box/config.json
Restart=on-failure
RestartSec=10s
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
```
- **'ExecStart': Specifies the command to start the service. It runs '/usr/local/bin/sing-box run -c /usr/local/etc/sing-box/config.json'.'/usr/local/bin/sing-box' is the absolute path of the sing-box program, '/usr/local/etc/sing-box/config.json' is the absolute path of the sing-box configuration file, and 'config.json' is the configuration file.**













