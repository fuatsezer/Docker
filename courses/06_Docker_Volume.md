# Docker Volume
Docker volume konteyneri kaldırsanız bile verileri depolar.
Postgresql konteynerini tekrar oluşturalım.
```console
[fuatsezer@localhost ~]$ docker run --name postgresql -e POSTGRES_USER=fuatsezer -e POSTGRES_PASSWORD=GBfvdcsxaz123 -d postgres:10
```
Postgresql shelline bağlanalım.
```console
[fuatsezer@localhost ~]$ docker container exec -it postgresql psql -U fuatsezer
```
train adında bir veritabanı oluşturalım.
```console
fuatsezer=# create database train;
```
train veritabanına girelim.
```console
fuatsezer=# \c train
```
Songs adlı bir tablo oluşturalım.
```console
train=# create table songs(id int, name varchar(50));
```
Tablonun içine kayıt girelim.
```console
train=# insert into songs values (1, 'Eye of the Tiger'), (2, 'In the Army Now'), (3, 'Billie Jean');
```
Bütün kayıtları görelim.
```console
train=# select * from songs;
```
Sheelden çıkalım.
```console
train=# \q
```
postgresql conteynerini durduralım
```console
[fuatsezer@localhost ~]$ docker container stop postgresql
```
postgresql konteynerinı silelim.
```console
[fuatsezer@localhost ~]$ docker container rm postgresql
```
Docker volume yaratma
```console
[fuatsezer@localhost ~]$ docker volume create v_postgresql_10
```
Volume'ü inceleme
```console
[fuatsezer@localhost ~]$ docker volume inspect v_postgresql_10
```
Konteyneri volume ile kurma
```console
docker run --name postgresql -e POSTGRES_USER=fuatsezer -e POSTGRES_PASSWORD=GBfvdcsxaz123 -v v_postgresql_10:/var/lib/postgresql/data -d postgres:10
```


















