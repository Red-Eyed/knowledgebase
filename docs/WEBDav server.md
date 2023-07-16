## Server: Install webdav server

`python3 -m pip install wsgidav cheroot lxml`

## Server: Run web dav server

`python3 -m wsgidav.server.server_cli -p60020 --root=/ --auth=anonymous -Hlocalhost`

## Client: Configure ssh config

Place next snippet to `~/.ssh/config`. If this file doesn't exist: create it  
```
Host webdav_server
  HostName 192.168.1.55 # ip of server
  User user 
  LocalForward 60020 localhost:60020 # port which will be forwarded from server to client
```

## Client: connect to webdav server

`ssh webdav_server -N`

## Client: mount directory

### Windows
1. Open File Explored : `Windows+E`
2. Right click on `This PC` -> `Map Network Drive`
3. Select drive letter
4. In folder, enter `http://localhost:600012`

### Linux
TBD: I don't need webdav for linux, there is `sshfs`
