# Docker Command Guide (বাংলা)

## 1. পরিচিতি
Docker হচ্ছে এমন একটি প্রযুক্তি যা অ্যাপ্লিকেশন ও তার ডিপেনডেন্সি একসঙ্গে প্যাক করে কন্টেইনার আকারে চালাতে দেয়। এতে সফটওয়্যার চলে একইভাবে যেকোনো সিস্টেমে যেখানে Docker ইনস্টল আছে।

## 2. Docker ইনস্টলেশন

### 2.1 Ubuntu-তে Docker ইনস্টল
```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
sudo add-apt-repository "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### 2.2 Docker সার্ভিস চালু
```bash
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

## 3. Docker বেসিক কমান্ড

### 3.1 `docker --version`
- কাজ: Docker ভার্সন দেখায়
- ব্যাখ্যা: `--version` ফ্ল্যাগ দিয়ে প্রোগ্রামের সংস্করণ আউটপুট হয়

```bash
docker --version
```

### 3.2 `docker info`
- কাজ: সিস্টেমে Docker সম্পর্কিত বিস্তারিত তথ্য দেখায়

```bash
docker info
```

### 3.3 `docker pull`
- কাজ: Docker Hub বা রেজিস্ট্রি থেকে ইমেজ ডাউনলোড করে
- উদাহরণ:
```bash
docker pull ubuntu:24.04
```
- ব্যাখ্যা: `ubuntu:24.04` হলো ইমেজ নাম ও ট্যাগ

### 3.4 `docker images`
- কাজ: লোকাল সিস্টেমে থাকা Docker ইমেজ দেখায়

```bash
docker images
```

### 3.5 `docker run`
- কাজ: নতুন কন্টেইনার চালায়
- উদাহরণ:
```bash
docker run --name my-ubuntu -it ubuntu:24.04 /bin/bash
```
- ব্যাখ্যা:
  - `--name my-ubuntu` : কন্টেইনার নাম
  - `-it` : ইন্টারঅ্যাক্টিভ টার্মিনাল
  - `ubuntu:24.04` : ইমেজ
  - `/bin/bash` : চালানোর কমান্ড

### 3.6 `docker ps`
- কাজ: চলমান কন্টেইনার দেখায়
- `-a` যোগ করলে সব কন্টেইনার দেখায়, শুধু চলমান নয়

```bash
docker ps -a
```

### 3.7 `docker stop`
- কাজ: চালু কন্টেইনার বন্ধ করে

```bash
docker stop my-ubuntu
```

### 3.8 `docker start`
- কাজ: বন্ধ কন্টেইনার আবার চালু করে

```bash
docker start my-ubuntu
```

### 3.9 `docker rm`
- কাজ: কন্টেইনার মুছে ফেলে
- সতর্কতা: আগে স্টপ করতে হবে

```bash
docker rm my-ubuntu
```

### 3.10 `docker rmi`
- কাজ: লোকাল Docker ইমেজ মুছে ফেলে

```bash
docker rmi ubuntu:24.04
```

## 4. ইমেজ ও কন্টেইনার ম্যানেজমেন্ট

### 4.1 `docker build`
- কাজ: Dockerfile থেকে ইমেজ তৈরি করে
- উদাহরণ:
```bash
docker build -t myapp:latest .
```
- ব্যাখ্যা:
  - `-t myapp:latest` : ট্যাগ দিয়ে নাম দাও
  - `.` : কারেন্ট ডিরেক্টরিতে `Dockerfile`

### 4.2 `docker commit`
- কাজ: চলমান কন্টেইনার থেকে নতুন ইমেজ তৈরি করে

```bash
docker commit my-ubuntu my-ubuntu-snapshot
```

### 4.3 `docker container prune`
- কাজ: সব স্টপ করা কন্টেইনার সরিয়ে দেয়

```bash
docker container prune
```

### 4.4 `docker image prune`
- কাজ: অপ্রয়োজনীয় ইমেজ মুছে দেয়

```bash
docker image prune -a
```
- ব্যাখ্যা: `-a` দিলে unused সব ইমেজ মুছে যায়

### 4.5 `docker system prune`
- কাজ: ব্যবহারহীন সব কন্টেইনার, ইমেজ, নেটওয়ার্ক ও বিল্ড ক্যাশ ক্লিন করে

```bash
docker system prune -a
```

## 5. নেটওয়ার্ক ও ভলিউম

### 5.1 `docker network ls`
- কাজ: Docker নেটওয়ার্ক তালিকা দেখায়

```bash
docker network ls
```

### 5.2 `docker network create`
- কাজ: নতুন নেটওয়ার্ক তৈরি করে

```bash
docker network create mynet
```

### 5.3 `docker network inspect`
- কাজ: নেটওয়ার্কের বিস্তারিত তথ্য দেখায়

```bash
docker network inspect mynet
```

### 5.4 `docker volume ls`
- কাজ: ভলিউম তালিকা দেখায়

```bash
docker volume ls
```

### 5.5 `docker volume create`
- কাজ: নতুন ভলিউম তৈরি করে

```bash
docker volume create mydata
```

### 5.6 `docker volume inspect`
- কাজ: ভলিউমের তথ্য দেখায়

```bash
docker volume inspect mydata
```

### 5.7 `docker run`-এ ভলিউম মাউন্ট
- উদাহরণ:
```bash
docker run --name my-nginx -d -p 8080:80 -v mydata:/var/www/html nginx:latest
```
- ব্যাখ্যা:
  - `-d` : ডিট্যাচড মোডে চালাবে
  - `-p 8080:80` : হোস্টের 8080 পোর্ট কন্টেইনারের 80 পোর্টে ম্যাপ করবে
  - `-v mydata:/var/www/html` : ভলিউম মাউন্ট

## 6. Dockerfile ও বিল্ড নীতি

### 6.1 Dockerfile বেসিক
- `FROM` : বেস ইমেজ
- `WORKDIR` : কাজের ডিরেক্টরি
- `COPY` : ফাইল কপি করে
- `RUN` : কমান্ড চালায়
- `CMD` : কন্টেইনার চালানোর ডিফল্ট কমান্ড

### 6.2 উদাহরণ Dockerfile
```Dockerfile
FROM ubuntu:24.04
RUN apt update && apt install -y python3 python3-pip
WORKDIR /app
COPY . /app
RUN pip3 install -r requirements.txt
CMD ["python3", "app.py"]
```

### 6.3 `docker build` ব্যাখ্যা
- `FROM ubuntu:24.04` : বেস ইমেজ
- `RUN apt update && apt install -y python3 python3-pip` : একাধিক কমান্ড একসঙ্গে
- `WORKDIR /app` : ওয়ার্কিং ডিরেক্টরি সেট
- `COPY . /app` : কারেন্ট ডিরেক্টরির সব কপি করে
- `CMD ["python3", "app.py"]` : ডিফল্ট রান কমান্ড

### 6.4 বিল্ড ইমেজ
```bash
docker build -t mypythonapp:1.0 .
```

## 7. Docker Compose

### 7.1 Compose ইনস্টল
```bash
sudo apt update
sudo apt install -y docker-compose
```

### 7.2 `docker-compose.yml` বেসিক
```yaml
version: '3.9'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: mydb
```

### 7.3 Compose কমান্ড

`docker-compose up -d`
- সার্ভিস গুলো ব্যাকগ্রাউন্ডে চালু করে

`docker-compose down`
- থেমে যাবে সব সার্ভিস ও নেটওয়ার্ক

`docker-compose ps`
- চলমান সার্ভিস দেখায়

`docker-compose logs web`
- `web` সার্ভিসের লগ দেখায়

## 8. উন্নত Docker কমান্ড

### 8.1 `docker exec`
- কাজ: রানের কন্টেইনারে কমান্ড চালায়

```bash
docker exec -it my-ubuntu /bin/bash
```

### 8.2 `docker logs`
- কাজ: কন্টেইনার লগ দেখায়

```bash
docker logs my-nginx
```

### 8.3 `docker inspect`
- কাজ: কন্টেইনার বা ইমেজের বিস্তারিত JSON তথ্য দেখায়

```bash
docker inspect my-ubuntu
```

### 8.4 `docker top`
- কাজ: কন্টেইনারের প্রক্রিয়া দেখায়

```bash
docker top my-ubuntu
```

### 8.5 `docker stats`
- কাজ: চলমান কন্টেইনারের রিসোর্স ব্যবহার দেখায়

```bash
docker stats
```

### 8.6 `docker cp`
- কাজ: হোস্ট ও কন্টেইনারের মধ্যে ফাইল কপি করে

```bash
docker cp ./localfile.txt my-ubuntu:/app/localfile.txt
```

### 8.7 `docker commit` ও `docker push`
- `docker commit` : কন্টেইনার থেকে ইমেজ তৈরি
- `docker push` : ইমেজ রেজিস্ট্রিতে আপলোড

উদাহরণ:
```bash
docker commit my-ubuntu myrepo/myimage:1.0
docker push myrepo/myimage:1.0
```

### 8.8 `docker login`
- কাজ: Docker Hub বা প্রাইভেট রেজিস্ট্রিতে লগইন করে

উদাহরণ:
```bash
docker login
```
- ব্যাখ্যা: ইউজারনেম ও পাসওয়ার্ড দিয়ে লগইন করলে `docker push` করা যায়

### 8.9 রিস্টার্ট পলিসি
- কাজ: কন্টেইনার ক্র্যাশ হলে আবার চালাতে সাহায্য করে

উদাহরণ:
```bash
docker run --name webapp --restart unless-stopped -d nginx:latest
```
- ব্যাখ্যা:
  - `--restart no` : ডিফল্ট, পুনরায় চালাবে না
  - `--restart always` : সিস্টেম রিস্টার্টের পরও চালু করবে
  - `--restart unless-stopped` : ম্যানুয়ালি স্টপ না করলে চালু রাখবে
  - `--restart on-failure:5` : ৫ বার ব্যর্থ হলে থামবে

### 8.10 `HEALTHCHECK` ও স্বাস্থ্য পরিদর্শন
- Dockerfile-এ `HEALTHCHECK` ব্যবহার করলে কন্টেইনারের স্বাস্থ্যের স্ট্যাটাস দেখা যায়

Dockerfile উদাহরণ:
```Dockerfile
FROM nginx:latest
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD curl -f http://localhost/ || exit 1
```

কন্টেইনারের স্বাস্থ্য দেখার জন্য:
```bash
docker ps
```
- `STATUS` কলামে `healthy`, `unhealthy`, বা `starting` দেখাবে

### 8.11 Multi-stage build
- কাজ: ছোট আকারের প্রোডাকশন ইমেজ তৈরি করতে সহায়তা করে

Dockerfile উদাহরণ:
```Dockerfile
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM debian:bookworm-slim
COPY --from=builder /app/myapp /usr/local/bin/myapp
CMD ["/usr/local/bin/myapp"]
```

### 8.12 `ARG` ও `ENV`
- `ARG` : বিল্ড টাইম ভেরিয়েবল
- `ENV` : রান টাইম পরিবেশ ভেরিয়েবল

Dockerfile উদাহরণ:
```Dockerfile
ARG APP_VERSION=1.0
ENV APP_ENV=production
RUN echo "Version=$APP_VERSION"
```

### 8.13 `.dockerignore`
- কাজ: বিল্ড কন্টেক্সট থেকে অপ্রয়োজনীয় ফাইল বাদ দেয়
- সাধারণ এন্ট্রি:
```
node_modules
.git
*.log
tmp/
```

### 8.14 নেটওয়ার্ক সংযোজন ও বিচ্ছিন্নতা
- `docker network connect` : চালমান কন্টেইনারে নেটওয়ার্ক যোগ করে
- `docker network disconnect` : কন্টেইনার থেকে নেটওয়ার্ক আলাদা করে

উদাহরণ:
```bash
docker network connect mynet my-ubuntu
docker network disconnect mynet my-ubuntu
```

### 8.15 লোগস ট্র্যাকিং
- `-f` : লাইন ফলো করে লাইভ আউটপুট দেখায়

উদাহরণ:
```bash
docker logs -f my-nginx
```

### 8.16 `docker compose` নতুন CLI
- `docker-compose` ছাড়াও নতুনভাবে `docker compose` ব্যবহার করা যায়

উদাহরণ:
```bash
docker compose up -d
docker compose down
```

## 9. কমান্ডের ব্যাখ্যা ও সাইন

- `-d` : detached mode, ব্যাকগ্রাউন্ডে চালায়
- `-it` : interactive + tty, কনটেইনারে টার্মিনাল পাওয়া
- `-p HOST:CONTAINER` : পোর্ট ম্যাপিং
- `-v HOST:CONTAINER` : ভলিউম বা ফোল্ডার মাউন্ট
- `--name` : কন্টেইনার নাম
- `-a` : all, সব দেখাতে
- `-f` : filter, নির্দিষ্ট মান খুঁজতে

## 10. Docker Troubleshooting ও টিপস

### 10.1 Docker daemon চালু ও স্ট্যাটাস
```bash
sudo systemctl status docker
```
- যদি `inactive` বা `failed` দেখায়, চালু কর:
```bash
sudo systemctl start docker
```

### 10.2 `docker system df`
- কাজ: Docker ডিস্ক ব্যবহার দেখায়

```bash
docker system df
```

### 10.3 `docker compose config`
- কাজ: Compose ফাইলের প্রসেসকৃত কনফিগারেশন দেখায়

```bash
docker compose config
```

### 10.4 `docker inspect` দিয়ে সমস্যা নির্ধারণ
```bash
docker inspect --format='{{.State.ExitCode}}' my-ubuntu
```
- `ExitCode` দেখলে কন্টেইনার কেন বন্ধ হলো বোঝা যায়

### 10.5 ডকার গ্রুপ সমস্যার সমাধান
- যদি `docker` কমান্ডে `permission denied` আসে, ব্যবহারকারীকে `docker` গ্রুপে যোগ করুন:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### 10.6 `docker compose logs --follow`
- লগ স্ট্রিম করতে সাহায্য করে

```bash
docker compose logs --follow
```

### 10.7 কন্টেইনার শেল পাওয়া
```bash
docker exec -it my-ubuntu /bin/bash
```

### 10.8 ডকার কম্পোজে এনভি ফাইল
- `docker-compose.yml` এ ব্যবহার:
```yaml
services:
  app:
    image: myapp:latest
    env_file:
      - .env
```
- `.env` ফাইলে রাখা হবে:
```
APP_ENV=production
DB_HOST=db
```

### 10.9 কন্টেইনার রিসোর্স সীমা
- CPU ও মেমরি সীমা দেয়ার উদাহরণ:
```bash
docker run -d --name myapp --cpus="1.5" --memory="512m" nginx:latest
```

### 10.10 সিকিউরিটি ও নেটওয়ার্ক
- `docker network inspect bridge` দিয়ে ডিফল্ট ব্রিজ নেটওয়ার্ক চেক করুন

```bash
docker network inspect bridge
```

## 11. Docker Compose উন্নত তথ্য

### 11.1 সার্ভিস রিস্টার্ট পলিসি
```yaml
services:
  web:
    image: nginx:latest
    restart: unless-stopped
```

### 11.2 বেধের ভলিউম
```yaml
services:
  db:
    image: mysql:8.0
    volumes:
      - dbdata:/var/lib/mysql
volumes:
  dbdata:
```

### 11.3 নেটওয়ার্ক তৈরি ও ব্যবহার
```yaml
networks:
  mynet:
    driver: bridge
services:
  web:
    image: nginx:latest
    networks:
      - mynet
```

### 11.4 Compose env_file
```yaml
services:
  app:
    env_file:
      - .env
```

### 11.5 `docker compose pull`
- কাজ: Compose ফাইলে উল্লেখিত ইমেজ সবাই ডাউনলোড করে

```bash
docker compose pull
```

### 11.6 `docker compose up --build`
- কাজ: Compose চালাতে গেলে ইমেজ রিলোড ও বিল্ড করবে

```bash
docker compose up --build -d
```

## 12. উপসংহার
এই ডকুমেন্টে Docker-র বেসিক থেকে অ্যাডভান্স কমান্ড, Dockerfile, Compose, নেটওয়ার্ক, ভলিউম, লগস এবং ট্রাবলশুটিং টিপস ব্যাখ্যা করা হয়েছে। এগুলো শিখলে Docker দিয়ে অ্যাপ্লিকেশন দ্রুত, নিরাপদ ও সহজে চালাতে পারবেন।