# DSOCKS
Docker hosted alpine based shadowsocks server. It is only 27MB(compressed).

## Configuration
Edit **conf/config.json**
```json
{
    "server":"0.0.0.0",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"123456",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```
The configuration file is mounted as a volume, you may edit and restart server without rebuilding.

## Start Server
```bash
docker-compose up -d
```

## Restart Server
```bash
docker-compose restart
```

## Stop Server
```bash
docker-compose stop
```

## Without docker-compose
```bash
docker run --restart=always -d -p 8388:8388 --name dsocks seancheung/dsocks:latest -p 8388 -k 123456 -m aes-256-cfb start

# stop, start and restart
docker stop dsocks
docker start dsocks
docker restart dsocks
```

## Linode StackScript, Vultr Startup Script(Boot)
```shellscript
#!/bin/bash

# envs
PORT=8388
PWD=123456
ENC=aes-256-cfb

# get docker
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh

# pull and run
if [ ! $(which docker) ]; then
  echo 'missing docker'
  exit 1
fi
docker run --restart=always -d -p $PORT:$PORT seancheung/dsocks:latest -p $PORT -k $PWD -m $ENC start
```
