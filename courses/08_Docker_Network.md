# Docker Network
Networkleri listeleme komutu:
```console
[fuatsezer@localhost ~]$ docker network ls
```
Networkün detayını inceleme komutu:
```console
[fuatsezer@localhost ~]$ docker network inspect bridge
```
Nginx Konteynerini başlatma
```console
[fuatsezer@localhost ~]$ docker run --rm --name nginx -p 8081:80 -d nginx
```
Bir ubuntu işletim sistemi olan alphine konteynerini başlatma
```console
[fuatsezer@localhost ~]$ docker run --rm --name alpine -it alpine /bin/sh
```
Docker network oluşturma:
```console
[fuatsezer@localhost ~]$ docker network create my-net
```
Nginx konteynerını my-net networküne bağlama
```console
[fuatsezer@localhost ~]$ docker network connect my-net nginx
```
Alpine'ı my-net networkü ile bağlama ve artık alpine shellinden nginexe ping atabiliyoruz
```console
[fuatsezer@localhost ~]$ docker run --rm --name alpine --network my-net -it alpine /bin/sh
```
Networkü kaldırma
```console
[fuatsezer@localhost ~]$ docker network rm my-net
```




