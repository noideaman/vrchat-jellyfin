# vrchat-jellyfin

a jellyfin client designed for vrchat

> [!IMPORTANT]
>
> ### Incomplete Project
>
> While this project is functional, it is not yet complete. The end goal is to have a link that can be pasted into the vrchat client, then use the jellyfin cast feature to control the player like a chromecast. This is not yet implemented, and the current implementation is a workaround.

handles requesting media from jellyfin in a format that can be played in vrchat, as well as proxying urls to bypass the risk of sharing a jellyfin api key

## Installation

install nodejs and npm

```bash
npm install
npm run build
```

## Usage

rename the `.env.example` file to `.env` and fill in the required fields.  

it's reccommended to use a process manager like pm2 to keep it running:

```bash
pm2 start dist/index.js --name vrc-jellyfin
pm2 save
```
make sure to do `pm2 startup` if you haven't already so it autostarts

go to the web interface, select media, and copy the link. paste the link into the vrchat client to play the media

## Docker

Navigate to the docker folder and use the 3 files there.

### Building
Use elevated permissions if it fails to build or run

```bash
docker build . -t vrchat-jellyfin
```

### Running

```bash
docker run -d \
--name vrchat-jellyfin \
--restart unless-stopped \
-p 4000:4000 \
-e JELLYFIN_HOST=<http[s]://URL> \
-e JELLYFIN_USERNAME=<USERNAME> \
-e JELLYFIN_PASSWORD=<PASSWORD> \
-e WEBSERVER_PORT=4000 \
vrchat-jellyfin:latest
```

## Progress

- [x] Jellyfin proxy 
- [x] Transcoding
- [ ] Subtitle Baking
- [ ] Subtitle/audio track selection
- [x] Temp Web interface
- [ ] Support for the jellyfin cast api
- [ ] Video Stream generation (splash screen with instructions, etc)
- [x] Docker
