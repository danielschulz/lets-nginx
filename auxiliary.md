
# Often used commands for Docker
date && \
    time docker build -t danielschulz/lets-nginx:tls-less . && \
    date

clear && docker run \
    -d \
    -p "20708:80" \
    -e DOMAIN="akpl.local;dsit.local" \
    -e UPSTREAM="hbr.org:443;heise.de:80" \
    --name revproxy \
    danielschulz/lets-nginx:tls-less && \
    sleep 3 && \
    docker logs revproxy

curl dsit.local:20708

curl akpl.local:20708

docker rm -f revproxy
