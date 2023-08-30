# Dockerfile Oluşturma
Aşağıdaki komut ile bir Dockerfile dosyası oluşturalım
```console
[fuatsezer@localhost docker]$ vim Dockerfile
```
Dockerfile'ın içine aşağıdakileri ekleyin.
```console
# Use alpine as base image
FROM alpine

# Install redis
RUN apk add --update redis

# Tell image what to do when start
CMD ["redis-server"]
```
Docker file'ı build etme
```console
[fuatsezer@localhost docker]$ docker image build -t fuatsezer/redis:2023-01 .
```
Yarattığımız docker imajı çalıştırma
```console
[fuatsezer@localhost docker]$ docker run --name myredis fuatsezer/redis:2023-01
```
