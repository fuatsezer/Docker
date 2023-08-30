# Port Mapping
Konteyner içindeki port ile dışarıdaki portu eşleştirme işlemidir.

Konteynere dışarıdan erişmeye çalışalım.
```console
[fuatsezer@localhost ~]$ psql -d train -U postgres
```
Port açarak konteyneri başlatma komutu
```console
[fuatsezer@localhost ~]$ docker run --name postgresql -e POSTGRES_USER=fuatsezer -e POSTGRES_PASSWORD=GBfvdcsxaz123 -v v_postgresql_10:/var/lib/postgresql/data -p 5433:5432 -d postgres:10
```
Postgresqli kurma komutu
```console
[fuatsezer@localhost ~]$ sudo yum install postgresql-server postgresql-contrib
```
Postgresql konteynerine dışarıdan bağlanma
```console
[fuatsezer@localhost ~]$ psql -h localhost -p 5433 -d train -U fuatsezer
```


