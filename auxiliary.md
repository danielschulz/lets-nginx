
# Often used commands for Docker
date && \
    time docker build -t danielschulz/lets-nginx:latest . && \
    date

clear && docker run \
    -d \
    -p "20602:80" \
    -p "20708:443" \
    -e DOMAIN="akpl.local;dsit.local" \
    -e UPSTREAM="hbr.org:443;heise.de:80" \
    -e EMAIL="ds@gru.ru" \
    -e STAGING="1" \
    -e TLS_RSA_SIZE_IN_BYTES="2048" \
    --name revproxy \
    danielschulz/lets-nginx:latest && \
    sleep 3 && \
    docker logs -f revproxy

curl dsit.local:20708

curl akpl.local:20708

docker rm -f revproxy
