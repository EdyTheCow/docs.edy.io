# CubeWorld

## Client
Client related instructions.

### Download
No account required, simply launch "Cube.exe" - https://link.edy.io/cubeworld

### Server
The 24/7 CubeWorld server IP:
```
cw.edy.io
```

## Server installtion
Server related instructions.
There are two ways of starting your own server. Installing everything manually or using docker.

### Docker

#### Requirements
- Valid picroma account
- Docker and Docker Compose

#### Installation

**Clone repository**
```
git clone https://github.com/BeefBytes/docker-cubeworld.git
```

**Start docker compose**
```
docker-compose up -d
```

**Attach to container**

For initial launch you'll be asked for picroma account credentials to download the required files. In order to enter the credentials you'll have to attach to the running container.
```
docker attach cubeworld_server
```
After successful download of required files you can simply exit the process using `CTRL+C`. To start the server simply re-run `docker-compose up -d` in the directory with docker-compose.yml.

### Manual
TODO