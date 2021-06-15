# SFTP

This is a SFTP-Image using openssh. This image is based on the offical [alpine](https://hub.docker.com/_/alpine)-Image (vers. 3.13.5).

## Configuration

The WORKDIR is `/app`. 
SFTP-Port is `4002`. 

You should map the following folders to get persistancy:
- /home (contains all homespaces including data)
- /app/conf (contains a file called `user.conf`)
- /app/ssh (contains host keys and sshd_conf)

### docker-compose example

```
volumes:
  sftp-data:
  sftp-config:
  sftp-ssh:

services:
  sftp:
    image: "devtanke/sftp:latest"
    restart: unless-stopped
    ports:
      - "4002:4002"
    volumes:
      - sftp-data:/home
      - sftp-config:/app/conf
      - sftp-ssh:/app/ssh
```

### Define users

To create users you can simply add them to the `user.conf` located in `/app/conf`. After importing the users, the file will get truncated. So be sure to store your credentials at a save place.

user.conf
```
username:somepassword
otheruser:someotherpassword
```

There is no default user on startup. Add a user before starting the container or simply restart after adding some credentials.
