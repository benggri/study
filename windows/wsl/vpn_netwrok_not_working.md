# 회사에서 WSL Ubuntu 를 설치했는데 VPN 연결하니까 Network 이 안돼요

- 제목 그대로 VPN 연결을 안하면 Network 가 정상적으로 동작하는데 VPN 을 연결하니까 안됨
- 어떤 천재가 만들어놓은 것이 있었다
- https://github.com/sakai135/wsl-vpnkit

```bash
# install dependencies
sudo apt-get install iproute2 iptables iputils-ping dnsutils wget

# download wsl-vpnkit and unpack
#VERSION=v0.4.x
#wget https://github.com/sakai135/wsl-vpnkit/releases/download/$VERSION/wsl-vpnkit.tar.gz
wget https://github.com/sakai135/wsl-vpnkit/releases/download/v0.4.1/wsl-vpnkit.tar.gz
tar --strip-components=1 -xf wsl-vpnkit.tar.gz \
    app/wsl-vpnkit \
    app/wsl-gvproxy.exe \
    app/wsl-vm \
    app/wsl-vpnkit.service
rm wsl-vpnkit.tar.gz

# run the wsl-vpnkit script in the foreground
sudo VMEXEC_PATH=$(pwd)/wsl-vm GVPROXY_PATH=$(pwd)/wsl-gvproxy.exe ./wsl-vpnkit
```

- 처음에만 위 shell 을 실행하고 2회차부터는

```bash
sudo VMEXEC_PATH=$(pwd)/wsl-vm GVPROXY_PATH=$(pwd)/wsl-gvproxy.exe ./wsl-vpnkit
```

- 이것만 하면된다 좋다!
