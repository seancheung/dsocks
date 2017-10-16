# DSOCKS
Docker hosted alpine based shadowsocks server. It is only 27MB(compressed) in size.

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
