# Bir Konteynerı Çalıştırmak, Durdurmak ve Bağlanmak
Bir konteyneri çalıştırmak için `run` komutu kullanılır.
```console
[fuatsezer@localhost ~]$ docker run --name postgresql -e POSTGRES_USER=fuatsezer -e POSTGRES_PASSWORD=GBfvdcsxaz123 -d postgres:10
```
Bir konteynerı durduran komut:
```console
[fuatsezer@localhost ~]$ docker container stop postgresql
```
Pull edilmiş var olan bir konteynerı yeniden başlatan komut:
```console
[fuatsezer@localhost ~]$ docker container start postgresql
```
Konteynerın içine giren (bağlanan) komut
```console
[fuatsezer@localhost ~]$ docker container exec -it postgresql /bin/bash
```
Postgresql'e bağlanan komut
```console
root@6c24210cc12b:/# psql -U fuatsezer
```
Konteyner shell'inden çıkan komut
Postgresql'e bağlanan komut
```console
root@6c24210cc12b:/# exit
```
Doğrudan postgresql shelline bağlanan komut:
```console
[fuatsezer@localhost ~]$ docker container exec -it postgresql psql -U fuatsezer
```
