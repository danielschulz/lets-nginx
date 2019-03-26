
# Often used commands for Docker
date && \
    time docker build -t danielschulz/lets-nginx:dev . && \
    date

clear && docker run \
    -d \
    -p "80:80" \
    -p "443:443" \
    -e DOMAIN="dsit.local" \
    -e UPSTREAM="hbr.org:443" \
    -e EMAIL="ds@gru.ru" \
    -e STAGING="1" \
    -e TLS_RSA_SIZE_IN_BYTES="2048" \
    --name revproxy \
    danielschulz/lets-nginx:latest && \
    sleep 3 && \
    docker logs -f revproxy

curl https://dsit.local:443
# curl -k https://dsit.local:443

docker rm -f revproxy
