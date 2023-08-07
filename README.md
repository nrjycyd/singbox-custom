### To check the system's kernel architecture, you can use the uname command with the -m option.
```
uname -m
```
- **amd64(x86_64、x64): Indicates the 64-bit kernel.**
- **386(i686 or i386): Indicates a 32-bit kernel.**
- **armv7l: Indicates a 32-bit ARM-based kernel.**
- **arm64(aarch64): Indicates a 64-bit ARM-based kernel.**
### The download URL for Go is [https://golang.org/dl/](https://go.dev/dl/).
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
### Install sing-box with option
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



