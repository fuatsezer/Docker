# Basit Bir Python Uygulamasına ait İmaj Oluşturma
Dockerfile oluşturalım.
```console
[fuatsezer@localhost ~]$ mkdir hello_python
[fuatsezer@localhost ~]$ vim Dockerfile
```
İçine Aşağıdakileri yazalım.
```console
FROM python:3.6

RUN mkdir /app

WORKDIR /app

COPY ./hello.py /app

CMD ["python", "hello.py"]
```
`hello.py` python kodunu yazalım.

```
[fuatsezer@localhost ~]$ vim hello.py
```
Python koduna aşağıdaki satırı ekleyelim
```console
print("Hello World from Docker container")
```
İmaj oluşturalım.
```console
[fuatsezer@localhost ~]$ docker build -t fuatsezer/hellopython:2023-01 .
```

Oluşturulan imajı run etme
```console
[fuatsezer@localhost ~]$ docker run --rm fuatsezer/hellopython:2023-01
```








