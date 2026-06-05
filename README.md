# Ubuntu ও Docker শেখার স্টেপ

এই README ফাইলটি তোমাকে ধাপে ধাপে Ubuntu ও Docker শেখার জন্য গাইড করবে। প্রতিটি বিভাগে কোন `.md` ফাইলটি পড়তে হবে, কোন কমান্ডগুলি প্র্যাকটিস করতে হবে, এবং কীভাবে শেখা উচিত তা ব্যাখ্যা করা আছে।

## 1. শেখা শুরু করার প্রস্তুতি

1. টার্মিনাল ওপেন করো।
2. `pwd`, `ls`, `cd` ইত্যাদি বেসিক কমান্ডগুলো প্র্যাকটিস করো।
3. যদি তুমি লিনাক্স নতুন, তাহলে আগে `ubuntu.md` ফাইল থেকে বেসিক কমান্ডগুলো পড়ো।

## 2. Ubuntu শেখার স্টেপ

### 2.1 বেসিক কমান্ড
- ফাইল ও ডিরেক্টরি পরিচালনা:
  - `pwd`, `ls`, `cd`, `mkdir`, `rm`, `cp`, `mv`
- টেক্সট ও ফাইল দেখার কমান্ড:
  - `cat`, `less`, `head`, `tail`, `grep`, `find`
- পারমিশন ও মালিকানা:
  - `chmod`, `chown`, `umask`
- প্যাকেজ ম্যানেজমেন্ট:
  - `sudo apt update`, `sudo apt install`, `sudo apt upgrade`

### 2.2 প্র্যাকটিস
1. `ubuntu.md` ফাইল পড়ে প্রতিটি কমান্ডের উদাহরণ করো।
2. একটি ছোট ফোল্ডার তৈরি করো, সেই ফোল্ডারের মধ্যে কিছু ফাইল কপি/মুভ/মুছো।
3. `ls -lah` ব্যবহার করে ফাইল পারমিশন দেখো।
4. `grep` দিয়ে কোন টেক্সটে নির্দিষ্ট শব্দ খুঁজে বের করো।

### 2.3 উন্নত Ubuntu কমান্ড
- `ps`, `top`, `htop`
- `df`, `du`
- `chmod`, `chown`
- `ping`, `ip addr show`, `ss`, `journalctl`
- `rsync`, `tar`, `zip`, `unzip`

### 2.4 প্র্যাকটিস
1. `ubuntu_advanced.md`-এ উল্লেখিত প্রতিটি প্রক্রিয়া কমান্ড একবার চালাও।
2. লোগ দেখো `journalctl -xe` দিয়ে।
3. নেটওয়ার্ক ইন্টারফেস চেক করো `ip addr show` দিয়ে।
4. `rsync` দিয়ে একটা ব্যাকআপ কপি তৈরি করো।

## 3. Docker শেখার স্টেপ

### 3.1 Docker ইন্সটল ও শুরু
- প্রথমে `docker.md` ফাইলের ইনস্টলেশন অংশ পড়ো।
- Docker সার্ভিস চালু করো:
  ```bash
  sudo systemctl enable docker
  sudo systemctl start docker
  sudo systemctl status docker
  ```

### 3.2 বেসিক Docker কমান্ড
- `docker --version`
- `docker pull`
- `docker images`
- `docker run`
- `docker ps -a`
- `docker stop`, `docker start`
- `docker rm`, `docker rmi`

### 3.3 প্র্যাকটিস
1. Docker Hub থেকে `ubuntu:24.04` ইমেজ টেনে নাও।
2. `docker run -it ubuntu:24.04 /bin/bash` দিয়ে একটি কন্টেইনারে ঢুকো।
3. কন্টেইনারের ভিতরে কিছু ফাইল তৈরি করো, বের হয়ে কন্টেইনার স্টপ করো।
4. `docker ps -a` দিয়ে কন্টেইনারের অবস্থা দেখো।

### 3.4 ইমেজ ও কন্টেইনার ম্যানেজমেন্ট
- Dockerfile তৈরি করে ইমেজ build করো।
- `docker container prune`, `docker image prune -a`, `docker system prune -a` ব্যবহার করে পরিষ্কারতা করো।
- ভলিউম ও নেটওয়ার্ক তৈরি করে দেখো।

### 3.5 Compose শেখা
- `docker-compose.yml` উদাহরণ দেখে একটি সিম্পল প্রজেক্ট তৈরি করো।
- `docker-compose up -d` চালাও এবং `docker-compose ps` দিয়ে চেক করো।
- `docker-compose logs web` দিয়ে লগ দেখো।

## 4. উন্নত Docker প্রশিক্ষণ

### 4.1 উন্নত টুলস
- `docker exec`
- `docker logs -f`
- `docker inspect`
- `docker stats`
- `docker cp`
- `docker login`

### 4.2 Dockerfile উন্নতি
- `HEALTHCHECK` যোগ করো।
- multi-stage build ব্যবহার করে কম ইমেজ তৈরি করো।
- `.dockerignore` ফাইল ব্যবহার করো।
- `ARG` ও `ENV` দিয়ে ভেরিয়েবল সেট করো।

### 4.3 Compose উন্নত
- `restart: unless-stopped` যোগ করো।
- ভলিউম রক্ষণাবেক্ষণ করো।
- কাস্টম নেটওয়ার্ক তৈরি করো।
- `.env` ফাইল ব্যবহার করে কনফিগারেশন চালাও।

## 5. শেখার চেকলিস্ট

- [ ] `ubuntu.md` বসিক কমান্ড পড়ে নেয়া
- [ ] `ubuntu_advanced.md` উন্নত কমান্ড অনুশীলন করা
- [ ] `docker.md` বেসিক Docker কমান্ড শিখে নেয়া
- [ ] Docker কন্টেইনার চালানো ও ম্যানেজ করা
- [ ] Dockerfile ও Docker Compose অনুশীলন করা
- [ ] Docker ট্রাবলশুটিং টিপস প্রয়োগ করা

## 6. টিপস

- প্রতিটি কমান্ডের কাজ বুঝে নাও, শুধু চালালে হবে না।
- ভুল হলে `man command` বা `command --help` দেখে আরো জানো।
- নতুন কমান্ড শেখার আগে ছোট উদাহরণ দিয়ে পরীক্ষা করো।
- ডকুমেন্টেশন ফাইলগুলোকে বারবার রিপিট করো।
- তুমি চাইলে আলাদা নোট তুলো এবং প্র্যাকটিস সংরক্ষণ করো।

---

এই README ফাইলটি তোমাকে Ubuntu ও Docker শেখার একটি সহজ রোডম্যাপ দিবে। প্রতিদিন একটু করে অনুশীলন করলে ভালো ধাপে শিখতে পারবে।