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

app = Flask(__name__)

@app.route("/")
def hello():
    return "<h1>Hello Flask App</h1>"
```
Flask uygulamasını çalıştırma
```console
[fuatsezer@localhost docker-compose-ex-2]$ flask run -h 0.0.0.0
```






