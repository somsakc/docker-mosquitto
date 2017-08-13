# docker-mosquitto

Porting official Eclipse mosquitto package to Docker image running on Raspberri Pi 2/3 (ARMv7 32-bit or arm32v7) platform.

## Directories
Three directories have been created in the image to be used for configuration, persistence storage and log.
- /mosquitto/config
- /mosquitto/data
- /mosquitto/log

## Usage
### Alternative 1:
Run Docker with minimal options by using default configuration supplied by Docker image.<br>
`$ docker run -d -e TZ=<timezone> -p 1883:1883 mbixtech/arm32v7-mosquitto`

For example, TZ=Asia/Bangkok

### Alternative 2:
Use a custom configuration file by mounting to local /mosquitto/config/mosquitto.conf file.<br>
`$ docker run -d -e TZ=<timezone> -p 1883:1883 -v mosquitto.conf:/mosquitto/config/mosquitto.conf mbixtech/arm32v7-mosquitto`

In /mosquitto.conf configuration file, it can be put the following parameters pointing specific directories.

persistence true
persistence_location /mosquitto/data/
log_dest file /mosquitto/log/mosquitto.log

### Alternative 3:
Map local directories to all specific directories of Docker container.<br>
`$ docker run -d -e TZ=<timezone> -p 1883:1883 -v config:/mosquitto/config -v data:/mosquitto/data -v log:/mosquitto/log mbixtech/arm32v7-mosquitto`

## Credits
Build Dockerfile base on original from https://github.com/eclipse/mosquitto/tree/master/docker git repository.

## Git Repository
Refer to https://github.com/somsakc/docker-mosquitto
