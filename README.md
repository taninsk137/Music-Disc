<img width="150" height="150" align="right" style="float: right; margin: 0 10px 0 0;" alt="music_disc" src="public/imgs/logo/logo2.png">

# Music Disc 

<a href="https://github.com/hmes98318/Music-Disc/releases"><img alt="GitHub package.json version" src="https://img.shields.io/github/package-json/v/hmes98318/Music-Disc?style=for-the-badge"></a> 
<a href="https://discord.js.org/"><img src="https://img.shields.io/badge/Discord.JS-v14-blue?style=for-the-badge&logo=DISCORD" /></a> 
<a href="https://nodejs.org/"><img src="https://img.shields.io/badge/Node.JS->=18.x-brightgreen?style=for-the-badge&logo=Node.js"></a> 
<a href="https://github.com/hmes98318/Music-Disc/blob/main/LICENSE"><img alt="GitHub" src="https://img.shields.io/github/license/hmes98318/Music-Disc?style=for-the-badge&color=brightgreen"></a>  

A discord music bot, supports **YouTube**, **Spotify**, **SoundCloud**, **Deezer** streams and web dashboard.  
Developed based on [**discord.js v14**](https://discord.js.org/#/), [**LavaShark**](https://lavashark.js.org/), [**Lavalink**](https://github.com/lavalink-devs/Lavalink/).  

### Features
* Stable
* Use Lavalink
* Web dashboard
* Local node
* Docker images

If you need the version of [**discord-player**](https://github.com/Androz2091/discord-player), please refer to this [**branch**](https://github.com/hmes98318/Music-Disc-discord-player).  

If you encounter any issues or would like to contribute to the community, please join our [Discord server](https://discord.gg/7rQEx7SPGr).  




## Deploying with node.js

### Clone the latest version of the repository
```
git clone -b v2.1.0 https://github.com/hmes98318/Music-Disc.git
```
or [**click here**](https://github.com/hmes98318/Music-Disc/releases) to download  


### Install the dependencies
install all the dependencies from [**package.json**](./package.json)  
```
npm install
```


### Add Lavalink node
Edit the [`nodelist.json`](./nodelist.json) file to add a [Lavalink](https://github.com/lavalink-devs/Lavalink) node.  
 * Use [public node](https://lavalink-list.darrennathanael.com/)  
 * or [host your own](https://blog.darrennathanael.com/post/how-to-lavalink/)  
 * or enable [local node setup](https://musicdisc.ggwp.tw/docs/Environment-variables-description#local-node)  

Please refer to this [**documentation**](https://lavashark.js.org/docs/server-config) for detailed information.  

```json
[
    {
        "id": "Node 1",
        "hostname": "localhost",
        "port": 2333,
        "password": "youshallnotpass"
    }
]
```


### Configure environment
Edit the file [**.env**](./.env) 
```env
# Discord Bot Token
BOT_TOKEN = "your_token"

# Admin of the bot (User ID)
BOT_ADMIN = ""

# Bot settings
BOT_NAME = "Music Disc"
BOT_PREFIX = "+"
BOT_STATUS = "online"
BOT_PLAYING = "+help | music"
BOT_EMBEDS_COLOR = "#FFFFFF"

# Volume settings
DEFAULT_VOLUME = 50
MAX_VOLUME = 100

# Auto leave channel settings
AUTO_LEAVE = true
AUTO_LEAVE_COOLDOWN = 5000

# Show voice channel updates
DISPLAY_VOICE_STATE = true

# Web dashboard settings
ENABLE_SITE = true
SITE_PORT = 33333
SITE_USERNAME = "admin"
SITE_PASSWORD = "password"

# Local Lavalink node
ENABLE_LOCAL_NODE = false
LOCAL_NODE_AUTO_RESTART = true
# LOCAL_NODE_DOWNLOAD_LINK = 
```

* [**Environment variables detailed description**](https://musicdisc.ggwp.tw/docs/Environment-variables-description)


### Running the script 
```
npm run start
```




## Deploying with Docker
**image link** : https://hub.docker.com/r/hmes98318/music-disc  

If you don't have any available nodes, you need to first start the server container using [Docker Compose](server/docker-compose.yml) in the server directory.  

### Start with Docker
Use the following command to start the container:  
Please put your **token** into the `TOKEN` variable.  
```
docker run -d \
  --name music-disc \
  -e TZ="Asia/Taipei" \
  -e BOT_TOKEN="your_token" \
  -e BOT_NAME="Music Disc" \
  -e BOT_PREFIX="+" \
  -e BOT_PLAYING="+help | music" \
  -e BOT_EMBEDS_COLOR="#FFFFFF" \
  -e DEFAULT_VOLUME=50 \
  -e MAX_VOLUME=100 \
  -e AUTO_LEAVE="true" \
  -e AUTO_LEAVE_COOLDOWN=5000 \
  -e DISPLAY_VOICE_STATE="true" \
  -e ENABLE_SITE=true \
  -e SITE_PORT=33333 \
  -e SITE_USERNAME="admin" \
  -e SITE_PASSWORD="000" \
  -e ENABLE_LOCAL_NODE=false \
  -e LOCAL_NODE_AUTO_RESTART=true \
  -v ./nodelist.json:/bot/nodelist.json \
  -v ./blacklist.json:/bot/blacklist.json \
  -p 33333:33333 \
  hmes98318/music-disc:2.1.0
```


### Start with Docker-Compose
Please put your **token** into the `TOKEN` variable.  
```yml
version: '3.8'
services:
  music-disc:
    image: hmes98318/music-disc:2.1.0
    container_name: music-disc
    restart: always
    environment:
      TZ: "Asia/Taipei"
      BOT_TOKEN: "your_token"
      BOT_NAME: "Music Disc"
      BOT_PREFIX: "+"
      BOT_PLAYING: "+help | music"
      BOT_EMBEDS_COLOR: "#FFFFFF"
      DEFAULT_VOLUME: 50
      MAX_VOLUME: 100
      AUTO_LEAVE: "true"
      AUTO_LEAVE_COOLDOWN: 5000
      DISPLAY_VOICE_STATE: "true"
      ENABLE_SITE: true
      SITE_PORT: 33333
      SITE_USERNAME: "admin"
      SITE_PASSWORD: "000"
      ENABLE_LOCAL_NODE: false
      LOCAL_NODE_AUTO_RESTART: true
    volumes:
      - ./nodelist.json:/bot/nodelist.json
      - ./blacklist.json:/bot/blacklist.json
    ports:
      - 33333:33333
```

#### Start the container  
```
docker-compose up -d
```
