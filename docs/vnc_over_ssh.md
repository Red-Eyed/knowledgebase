# Secure VNC over SSH on headless linux server via web browser

![](../attachements/vnc_in_browser.png)

This guide provides instructions for setting up a secure VNC server on a headless linux server via web browser using SSH port forwarding.

## Prerequisites

- **Server**: any linux (I tested with [debian lxde](https://wiki.debian.org/LXDE)) with SSH access with [LXDE](https://help.ubuntu.com/community/LXDE) or [XFCE](https://www.xfce.org/) DE.
- **Client**: any machine (linux/mac/windows) with SSH client.
- `sudo` access to **server**.

## Step 0: (Optional )\[Client\] generate ssh key pair

Using SSH key pairs over plain passwords provides the following benefits:

1. **Security**: SSH keys are cryptographically stronger than passwords, making brute-force attacks practically impossible.
2. **Convenience**: Keys allow for passwordless authentication, streamlining the login process without repeated password entry.
3. **Automation**: Keys facilitate automated processes, such as scripts, by allowing secure, passwordless SSH connections.
4. **Access Control**: Keys can be easily added or revoked for secure access management without changing passwords.

How to generate them:

1. generate keys:
   - `ssh-keygen`
2. copy public key to server:
   - linux/mac: `ssh-copy-id SERVER_USER@SERVER_IP`
   - windows: use [this guide](./ssh-copy-id%20for%20windows.md)

## Step 1: \[Server\] Install a VNC server on linux

1. 

NOTE: password could be as simple as possible, all trafic is secured by ssh tunnel anyway.

6. 

## Step 2: \[Server\] Configure VNC to start a desktop environment

1. 

## Step 3: \[Server\] Set up WEB GUI to access VNC from web browser

```bash
git clone https://github.com/novnc/noVNC
cd noVNC
./utils/novnc_proxy --vnc localhost:5901 --listen localhost:6081
```

## Step 4: \[Client\] Set Up SSH tunneling

```bash
 ssh -L 6081:localhost:6081 USER@SERVER_IP -N
```

## Step 5: \[Client\]  Connect to VNC

Open link: http://localhost:6081/vnc.html

# Summary

Let's summarize what's going on

- Start **VNC** server on linux machine `localhost:5901` which is not accessible from outside
- Start **noVNC** server (server which makes to use any browser as a client) on linux machine `localhost:6081` which is aslo not accessible from outside
- Create ssh **encrypted** tunnel `ssh -L 6081:localhost:6081 USER@SERVER_IP -N` between your client and server. It's called [local port forwarding](https://en.wikipedia.org/wiki/Port_forwarding#Local_port_forwarding). Again: all traffic which goes from server side to client via `6081` port is **strongly encrypted**.
- Accessing linux server desktop environment via any browser.