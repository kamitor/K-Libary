
https://jellyfin.org/docs/general/installation/container/
https://www.reddit.com/r/jellyfin/comments/erccwn/jellyfin_on_docker_for_dummies/

mkdir /path/to/config
mkdir /path/to/cache

docker pull jellyfin/jellyfin

```

docker run -d \
 --name jellyfin \
 --user uid:gid \
 --net=host 
 --volume /home/chris/Downloads/jellyfish/config:/config \ 
 --volume /home/chris/Downloads/jellyfish/cache:/cache \ 
 --mount type=bind,source=/home/chris/Downloads/jellyfish/media,target=/media \
 --restart=unless-stopped \
 jellyfin/jellyfin

```

/home/chris/Downloads/jellyfish/config
/home/chris/Downloads/jellyfish/cache
/home/chris/Downloads/jellyfish/media
/home/chris/Downloads/jellyfish/media2

version: '3.5'
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    user: uid:gid
    network_mode: 'host'
    volumes:
      - /home/chris/Downloads/jellyfish/config:/config
      - /home/chris/Downloads/jellyfish/cache:/cache
      - /home/chris/Downloads/jellyfish/media:/media
      - /home/chris/Downloads/jellyfish/media2:ro
    restart: 'unless-stopped'
    # Optional - alternative address used for autodiscovery
    environment:
      - JELLYFIN_PublishedServerUrl=http://example.com
    # Optional - may be necessary for docker healthcheck to pass if running in host network mode
    extra_hosts:
      - "host.docker.internal:host-gateway"

Host ip Feungirola 192.168.18.14 
Port : 8096

Host Router IP: 192.168.18.1
user: root
pass: FeungirolaChrisKip!

