# Docker Komut Satırı
Docker komut formatı: `docker options komut`
Docker'ın versiyonunu görmek için aşağıdaki komutu çalıştırın.
```console
[fuatsezer@localhost ~]$ docker version
```
Örnek bir docker komutu:
```console
[fuatsezer@localhost ~]$ docker run hello-world
```
Çalışan konteynerları gösteren komut
```console
[fuatsezer@localhost ~]$ docker ps
```
Çalışıp duran konteynerları gösteren komut
```console
[fuatsezer@localhost ~]$ docker ps -a
```
Örnek bir konteyner (busybox) çalıştırma komutu:
```console
[fuatsezer@localhost ~]$ docker run busybox ping -c 5 8.8.8.8
```











