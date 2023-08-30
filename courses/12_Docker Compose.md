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






