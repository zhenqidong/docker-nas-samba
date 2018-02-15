# Docker Image for SAMBA 4 - NAS Container

Based on Debian

## Run Container

```
$ docker build -t mynas .
$ docker run -it --name nas -p 445:445 -p 137:137 -p 138:138 -p 139:139 -v /etc/localtime:/etc/localtime:ro -v /etc/timezone:/etc/timezone:ro --hostname=Servername -v $(pwd)/multiuser.conf:/conf/multiuser.conf:z -v /path/to/:/home/test mynas
```

## Testing notes:
    1. :ro may not work on centos, use Z option instead
    2. aws blocks all the samba ports by default
    3. smb port used by windows isn't configurable
    4. use Z for mutiuser.conf binding, otherwise the file isn't readable inside docker
    5. the smb.conf has missed 'guest account = xxx ' in general section
    6. public = guest ok
    7. WARNING: Ignoring invalid value 'share' for parameter 'security' - share not in samba4 any more
    8. map to guest = Bad Password _# this is the key to make public share works
    
## commands:
    1. smbclient //host/share
