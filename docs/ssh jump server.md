Here is the example configuration of access to work PC connected to home openvpn server 
```shell
Host ubuntu-rpi
  HostName ubuntu-rpi
  User ubuntu
  RequestTTY yes
  RemoteCommand tmux new-session -A -s main

Host router
  HostName 192.168.1.1
  User admin
  Port 8888

Host srukr-redeyed-pc
  HostName 10.8.0.42
  User redeyed
  ProxyJump router
  RequestTTY yes
  PasswordAuthentication yes
  RemoteCommand tmux new-session -A -s main
  LocalForward 60012 localhost:60012

```

Now I can access `srukr-redeyed-pc` just type `ssh srukr-redeyed-pc`
