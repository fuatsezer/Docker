# Docker Compose
Birden fazla konteynerlı projeler için kullanılır.
## Docker Compose ile Çoklu Konteyner Uygulaması Geliştirmek
### Pip Kurulumu
Pip'i kurmak için aşağıdaki komutları çalıştırın
```console
[fuatsezer@localhost docker-compose-ex-2]$ sudo yum install epel-release
[fuatsezer@localhost docker-compose-ex-2]$ sudo yum install python-pip
[fuatsezer@localhost docker-compose-ex-2]$ pip --version
```
### Flask Kurulumu
```console
[fuatsezer@localhost docker-compose-ex-2]$ pip install flask
```
### Redis Kurulumu
```console
[fuatsezer@localhost docker-compose-ex-2]$ pip install redis
```
### Flask'in çalışacağı python kodunu yazma.
`app.py` adlı bir dosya oluşturun ve aşağıdaki kodları yazın
```python
import redis
from flask import Flask
import time

app = Flask(__name__)

cache = redis.Redis(host="localhost",port=6379)

def get_hit_count():
    retries=5
    while True:
        try: 
            return cache.incr("hits")
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)



@app.route("/")
def hello():
    count = get_hit_count()
    return "<h1>Hello Flask App. You have visited {} times</h1>".format(count)

if __name__ == '__main__':
    app.run(host='0.0.0.0', debug=True, port=5000)
```
Flask uygulamasını çalıştırma
```console
[fuatsezer@localhost docker-compose-ex-2]$ flask run -h 0.0.0.0
```

## Docker Compose Kurulumu 

Docker Compose'u linuxe kurmak için aşağıdaki komutları çalıştıralım
```console
[fuatsezer@localhost docker-compose-ex-2]$ sudo yum install docker-compose-plugin
[fuatsezer@localhost docker-compose-ex-2]$ sudo curl -SL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
[fuatsezer@localhost docker-compose-ex-2]$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
[fuatsezer@localhost docker-compose-ex-2]$ sudo chmod 755 /usr/local/bin/docker-compose
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose version
>> Docker Compose version v2.20.3
```
app.py dosyasında aşağıdaki gibi değiştirelim
```python
import redis
from flask import Flask
import time

app = Flask(__name__)

cache = redis.Redis(host="redis",port=6379)

def get_hit_count():
    retries=5
    while True:
        try: 
            return cache.incr("hits")
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)



@app.route("/")
def hello():
    count = get_hit_count()
    return "<h1>Hello Flask App. You have visited {} times</h1>".format(count)

if __name__ == '__main__':
    app.run(host='0.0.0.0', debug=True, port=5000)
```
requirements.txt dosyası oluşturalım ve içine gerekli kütüphaneleri yazalım flask ve redis
```console
[fuatsezer@localhost docker-compose-ex-2]$ vim requirements.txt
```
Dockerfile'ı oluşturalım ve aşağıdakileri yazalım
```console
[fuatsezer@localhost docker-compose-ex-2]$ touch Dockerfile
"""""""
FROM centos/python-36-centos7

WORKDIR /code

ENV FLASK_APP app.py

ENV FLASK_RUN_HOST 0.0.0.0

COPY requirements.txt requirements.txt

RUN pip install --upgrade pip && pip install -r requirements.txt

EXPOSE 5000

COPY . .

CMD ["flask", "run"]
""""""
```
Docker imajı yaratalım
```console
[fuatsezer@localhost docker-compose-ex-2]$ docker build .
```
docker-compose.yml dosyasını oluşturalım ve içine aşağıdakileri yazalım.
```console
[fuatsezer@localhost docker-compose-ex-2]$ touch docker-compose.yml
"""""""
---
services:
  redis:
    image: redis


  web:
    build: "."
    ports: 
      - "5000:5000"
version: "3"
""""""
```
docker-compose'u built ve up edelim.
```console
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose build
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose up -d
```
Çalışan docker-composeları listeleme
```console
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose ps
```
docker compose'un çıktısına bakma
```console
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose logs
```
Docker compose'u durdurma
```console
[fuatsezer@localhost docker-compose-ex-2]$ docker-compose down
```




