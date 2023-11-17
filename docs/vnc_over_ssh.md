# VNC Over SSH on headless linux server

This guide provides instructions for setting up a secure VNC session to a headless linux server from a Windows/linux client using SSH port forwarding.

## Prerequisites

- A headless linux server with SSH access.
- A windows/linux client with an SSH client (like PuTTY on Windows or any other) and a VNC viewer installed.
- Administrative access to both systems.

## Step 1: Install a VNC Server on linux

1. Open a terminal on your linux server.
2. Update your package list:

   ```bash
   sudo apt update
   ```

3. Install the VNC server:

   ```bash
   sudo apt install tightvncserver
   ```

4. Set a VNC access password:

   ```bash
   vncpasswd
   ```

5. Start the VNC server:

   ```bash
   vncserver
   ```

## Step 2: Configure VNC to Start a Desktop Environment

1. Stop the VNC server to configure it:

   ```bash
   vncserver -kill :1
   ```

2. Edit the `~/.vnc/xstartup` file to start a desktop environment:

   ```bash
   nano ~/.vnc/xstartup
   ```

3. Add these lines to the file:

   ```bash
   #!/bin/sh
   export XKL_XMODMAP_DISABLE=1
   unset SESSION_MANAGER
   unset DBUS_SESSION_BUS_ADDRESS
   [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
   [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
   gnome-shell &
   # startxfce4 &
   ```

4. Make the `xstartup` file executable:

   ```bash
   chmod +x ~/.vnc/xstartup
   ```

5. Restart the VNC server:

   ```bash
   vncserver
   ```

## Step 3: Set Up SSH Tunneling on client

```bash
 ssh -L 5901:localhost:5901 USER@SERVER_IP -N
```

## Step 4: Connect Using a VNC Client

You can use any VNC client from the list bellow. Or find any other you like
- [TigerVNC](https://tigervnc.org/) (Windows/linux)
- [RemminaVNC](https://remmina.org/remmina-vnc/) (linux)

## Step 5: Secure Your VNC Session

Ensure that encryption is optional on the VNC server for compatibility:

```bash
gsettings set org.gnome.Vino require-encryption false
```
