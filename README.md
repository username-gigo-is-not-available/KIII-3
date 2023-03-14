# KIII-3

```
$ cd flask-app
$ ls -l
total 16
-rw-r--r-- 1 gigo gigo 158 Mar 14 10:36 Dockerfile
-rw-r--r-- 1 gigo gigo 333 Mar 14 10:36 app.py
-rw-r--r-- 1 gigo gigo 170 Mar 14 10:43 docker-compose.yml
-rw-r--r-- 1 gigo gigo  12 Mar 14 10:36 requirements.txt
$ nano Dockerfile
$ cat Dockerfile
FROM python:3.9
LABEL maintainer="james@example.com"
ENV REFRESHED_AT 2016-08-01

ADD . /flask-app

WORKDIR /flask-app

RUN pip install -r requirements.txt
$ nano docker-compose.yml
$ cat docker-compose.yml
version: '3'
services:
  web:
    image: flask-app
    command: python app.py
    ports:
      - "5000:5000"
    volumes:
      - .:/flask-app
  redis:
    image: redis
```
### $ docker build -t flask-app .
### $ docker images
```
$ docker images
REPOSITORY                TAG          IMAGE ID       CREATED          SIZE
flask-app                latest       8f8fdd1c9658   18 seconds ago   921MB
gigo123/static_web       latest       d5e6d18fb95f   37 hours ago     168MB
ubuntu                   latest       74f2314a03de   13 days ago      77.8MB
ubuntu                   18.04        b89fba62bc15   13 days ago      63.1MB
wurstmeister/kafka       2.11-2.0.0   568143d73a6b   4 years ago      339MB
wurstmeister/zookeeper   3.4.6        6fe5551964f5   7 years ago      451MB
```
### $ nano docker-compose.yml
### $ cat docker-compose.yml
```
version: '3'
services:
  web:
    build: /home/gigo/flask-app
    image: flask-app
    command: python app.py
    ports:
      - "5000:5000"
    volumes:
      - .:/flask-app
  redis:
    image: redis
 ```
### $ docker compose up 
```
$ docker compose up
 ⠿ redis Pulled                                                                                                15.8s
   ⠿ 3f9582a2cbe7 Pull complete                                                                                10.8s
   ⠿ 241c2d338588 Pull complete                                                                                11.1s
   ⠿ 89515d93a23e Pull complete                                                                                11.2s
   ⠿ 65e8ba9473fe Pull complete                                                                                11.6s
   ⠿ 585124038cab Pull complete                                                                                11.7s
   ⠿ b483de716a47 Pull complete                                                                                11.9s
 ⠿ web Warning                                                                                                  3.0s
[+] Building 22.7s (10/10) FINISHED
 => [internal] load build definition from Dockerfile                                                           11.5s
 => => transferring dockerfile: 195B                                                                            0.0s
 => [internal] load .dockerignore                                                                              11.5s
 => => transferring context: 2B                                                                                 0.0s
 => [internal] load metadata for docker.io/library/python:3.9                                                   2.4s
 => [auth] library/python:pull token for registry-1.docker.io                                                   0.0s
 => [internal] load build context                                                                               0.0s
 => => transferring context: 872B                                                                               0.0s
 => CACHED [1/4] FROM docker.io/library/python:3.9@sha256:940ea29f268668b00305e22a93e3cbd0f3b05a221716a134f55a  0.0s
 => [2/4] ADD . /flask-app                                                                                      0.0s
 => [3/4] WORKDIR /flask-app                                                                                    0.1s
 => [4/4] RUN pip install -r requirements.txt                                                                   8.2s
 => exporting to image                                                                                          0.3s
 => => exporting layers                                                                                         0.2s
 => => writing image sha256:4341b93b6f1495435bf9afe73dcc4dd64d838993be8c633257878b0a7478b373                    0.0s
 => => naming to docker.io/library/flask-app                                                                    0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
[+] Running 3/3
 ⠿ Network flask-app_default    Created                                                                         0.1s
 ⠿ Container flask-app-redis-1  Created                                                                         0.2s
 ⠿ Container flask-app-web-1    Created                                                                         0.2s
Attaching to flask-app-redis-1, flask-app-web-1
flask-app-redis-1  | 1:C 14 Mar 2023 10:59:04.652 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
flask-app-redis-1  | 1:C 14 Mar 2023 10:59:04.652 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=1, just started
flask-app-redis-1  | 1:C 14 Mar 2023 10:59:04.652 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
flask-app-redis-1  | 1:M 14 Mar 2023 10:59:04.652 * monotonic clock: POSIX clock_gettime
flask-app-redis-1  | 1:M 14 Mar 2023 10:59:04.653 * Running mode=standalone, port=6379.
flask-app-redis-1  | 1:M 14 Mar 2023 10:59:04.653 # Server initialized
flask-app-redis-1  | 1:M 14 Mar 2023 10:59:04.653 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
flask-app-redis-1  | 1:M 14 Mar 2023 10:59:04.671 * Ready to accept connections
flask-app-web-1    |  * Serving Flask app 'app'
flask-app-web-1    |  * Debug mode: on
flask-app-web-1    | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
flask-app-web-1    |  * Running on all addresses (0.0.0.0)
flask-app-web-1    |  * Running on http://127.0.0.1:5000
flask-app-web-1    |  * Running on http://172.19.0.3:5000
flask-app-web-1    | Press CTRL+C to quit
flask-app-web-1    |  * Restarting with stat
flask-app-web-1    |  * Debugger is active!
flask-app-web-1    |  * Debugger PIN: 165-375-168
```
### docker ps -a
```
$ docker ps -a
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS                      PORTS                                  NAMES
f75eb809599e   flask-app                       "python app.py"          2 minutes ago   Exited (0) 16 seconds ago                                          flask-app-web-1
789211be9f1e   redis                           "docker-entrypoint.s…"   2 minutes ago   Exited (0) 16 seconds ago                                          flask-app-redis-1
40bf174ba077   python                          "app.py"                 6 minutes ago   Created                     0.0.0.0:5000->5000/tcp                 flask-app
0e6d2d7714f5   gigo123/static_web              "/bin/bash"              36 hours ago    Exited (0) 36 hours ago                                            loving_tharp
c032dea298f8   ubuntu:18.04                    "/bin/bash"              5 days ago      Exited (0) 5 days ago                                              new_container
8d3c1aee8a10   ubuntu                          "/bin/bash"              5 days ago      Exited (0) 5 days ago                                              bob_the_container
b5e6f9280dd5   ubuntu                          "/bin/bash"              5 days ago      Exited (0) 5 days ago                                              clever_kepler
016f2c53b0be   wurstmeister/kafka:2.11-2.0.0   "start-kafka.sh"         6 weeks ago     Exited (255) 7 days ago     0.0.0.0:9092->9092/tcp, 9093/tcp       e-kafka-1
54d2e38c991d   wurstmeister/zookeeper:3.4.6    "/bin/sh -c '/usr/sb…"   6 weeks ago     Exited (255) 7 days ago     22/tcp, 2181/tcp, 2888/tcp, 3888/tcp   e-zookeeper-1
c97b8b3af058   wurstmeister/kafka:2.11-2.0.0   "start-kafka.sh"         6 weeks ago     Exited (1) 6 weeks ago                                             bold_banach
```
### $ docker compose up -d
```
$ docker compose up -d
[+] Running 2/2
 ⠿ Container flask-app-redis-1  Started                                                                         2.6s
 ⠿ Container flask-app-web-1    Started                                                                         2.5s
 ```
 ### $ curl 127.0.0.1:5000
 ```
 $ curl 127.0.0.1:5000
 Hello Docker Book reader! I have been seen b'3' times
 ```
 ### $ docker compose ps
 ```
 $ docker compose ps
NAME                COMMAND                  SERVICE             STATUS              PORTS
flask-app-redis-1   "docker-entrypoint.s…"   redis               running             6379/tcp
flask-app-web-1     "python app.py"          web                 running             0.0.0.0:5000->5000/tcp
```
### $ docker compose logs
```
$ docker compose logs
flask-app-redis-1  | 1:C 14 Mar 2023 11:22:55.748 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
flask-app-web-1    |  * Serving Flask app 'app'
flask-app-web-1    |  * Debug mode: on
flask-app-web-1    | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
flask-app-web-1    |  * Running on all addresses (0.0.0.0)
flask-app-web-1    |  * Running on http://127.0.0.1:5000
flask-app-web-1    |  * Running on http://172.19.0.3:5000
flask-app-web-1    | Press CTRL+C to quit
flask-app-web-1    |  * Restarting with stat
flask-app-web-1    |  * Debugger is active!
flask-app-web-1    |  * Debugger PIN: 165-375-168
flask-app-web-1    |  * Serving Flask app 'app'
flask-app-web-1    |  * Debug mode: on
flask-app-web-1    | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
flask-app-web-1    |  * Running on all addresses (0.0.0.0)
flask-app-web-1    |  * Running on http://127.0.0.1:5000
flask-app-web-1    |  * Running on http://172.19.0.3:5000
flask-app-web-1    | Press CTRL+C to quit
flask-app-web-1    |  * Restarting with stat
flask-app-web-1    |  * Debugger is active!
flask-app-web-1    |  * Debugger PIN: 165-375-168
flask-app-web-1    | 172.19.0.1 - - [14/Mar/2023 11:23:04] "GET / HTTP/1.1" 200 -
flask-app-web-1    | 172.19.0.1 - - [14/Mar/2023 11:23:04] "GET /favicon.ico HTTP/1.1" 404 -
flask-app-web-1    | 172.19.0.1 - - [14/Mar/2023 11:23:08] "GET / HTTP/1.1" 200 -
flask-app-web-1    | 172.19.0.1 - - [14/Mar/2023 11:23:27] "GET / HTTP/1.1" 200 -
flask-app-redis-1  | 1:C 14 Mar 2023 11:22:55.748 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=1, just started
flask-app-redis-1  | 1:C 14 Mar 2023 11:22:55.748 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.748 * monotonic clock: POSIX clock_gettime
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * Running mode=standalone, port=6379.
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 # Server initialized
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * Loading RDB produced by version 7.0.9
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * RDB age 1298 seconds
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * RDB memory usage when created 0.82 Mb
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * Done loading RDB, keys loaded: 0, keys expired: 0.
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * DB loaded from disk: 0.000 seconds
flask-app-redis-1  | 1:M 14 Mar 2023 11:22:55.749 * Ready to accept connections
```
### $ docker compose stop
```
$ docker compose stop
 ⠿ Container flask-app-web-1    Stopped                                                                         0.6s
 ⠿ Container flask-app-redis-1  Stopped                                                                         0.7s
```
### $ docker compose ps
```
$ docker compose ps
NAME                COMMAND                  SERVICE             STATUS              PORTS
flask-app-redis-1   "docker-entrypoint.s…"   redis               exited (0)
flask-app-web-1     "python app.py"          web                 exited (0)
```
### $ docker compose rm
```
$ docker compose rm
? Going to remove flask-app-redis-1, flask-app-web-1 Yes
[+] Running 2/0
 ⠿ Container flask-app-web-1    Removed                                                                         0.1s
 ⠿ Container flask-app-redis-1  Removed
```
### $ docker compose ps
```
$ docker compose ps
NAME                COMMAND             SERVICE             STATUS              PORTS
```
