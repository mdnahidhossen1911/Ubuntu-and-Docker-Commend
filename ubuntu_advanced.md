# Ubuntu Advanced Command Guide (বাংলা)

## 1. ফাইল এক্সেস ও পারমিশন

### 1.1 `ls -l`
- `ls` : লিস্ট, ডিরেক্টরি বা ফাইল দেখায়
- `-l` : লং ফরম্যাট, ফাইলের বিস্তারিত তথ্য দেখায়

উদাহরণ:
```bash
ls -l /var/www
```
- প্রথম কলাম: পারমিশন (rwx rwx rwx)
- দ্বিতীয় কলাম: লিঙ্কের সংখ্যা
- তৃতীয় কলাম: মালিক
- চতুর্থ কলাম: গ্রুপ
- পরের কলাম: ফাইল সাইজ, তারিখ, নাম

### 1.2 `chmod`
- পূর্ণ রূপ: change mode
- কাজ: ফাইল বা ডিরেক্টরির পারমিশন বদলায়

উদাহরণ:
```bash
chmod 755 /var/www/html
```
ব্রেকডাউন:
- `chmod` : কমান্ড নাম
- `755` : এনোমেরিক পারমিশন
  - `7` = 4+2+1 = read+write+execute (owner)
  - `5` = 4+1 = read+execute (group)
  - `5` = read+execute (others)
- `/var/www/html` : টার্গেট ফাইল/ডিরেক্টরি

অন্য উদাহরণ:
```bash
chmod u+rwx,g+rx,o-rwx script.sh
```
ব্রেকডাউন:
- `u` : user/owner
- `g` : group
- `o` : others
- `+rwx` : পড়া, লেখা, চালানোর অনুমতি যোগ করা
- `-rwx` : অনুমতি বাদ দেওয়া

### 1.3 `chown`
- পূর্ণ রূপ: change owner
- কাজ: মালিক বা গ্রুপ বদলায়

উদাহরণ:
```bash
sudo chown www-data:www-data /var/www/html -R
```
ব্রেকডাউন:
- `sudo` : প্রশাসনিক অধিকার দিয়ে চালানো
- `chown` : মালিক পরিবর্তন কর
- `www-data:www-data` : মালিক ও গ্রুপ
- `/var/www/html` : টার্গেট
- `-R` : রিকারসিভ, সব ভেতরের ফাইল/ফোল্ডারেও প্রযোজ্য

### 1.4 `umask`
- কাজ: ডিফল্ট পারমিশন সেট করে নতুন ফাইল/ফোল্ডারের জন্য

উদাহরণ:
```bash
umask 022
```
ব্রেকডাউন:
- `umask` : ইউ-নিভার্সাল মাস্ক
- `022` : নতুন ফাইল/ফোল্ডার থেকে গ্রুপ ও অন্যদের লেখার অনুমতি বাদ পড়বে

---

## 2. ইউজার তৈরি ও রুট অ্যাক্সেস

### 2.1 `adduser`
- কাজ: নতুন ইউজার তৈরি করে

উদাহরণ:
```bash
sudo adduser newuser
```
ব্রেকডাউন:
- `sudo` : প্রশাসনিক অধিকার
- `adduser` : নতুন ব্যবহারকারী তৈরি
- `newuser` : ব্যবহারকারীর নাম

### 2.2 `useradd`
- `adduser` এর চেয়ে কম লার্জ, কনফিগারেশন ম্যানুয়ালি করতে হয়

উদাহরণ:
```bash
sudo useradd -m -s /bin/bash newuser
```
- `-m` : হোম ডিরেক্টরি তৈরি
- `-s /bin/bash` : ডিফল্ট শেল সেট

### 2.3 `passwd`
- কাজ: ব্যবহারকারীর পাসওয়ার্ড সেট করে

উদাহরণ:
```bash
sudo passwd newuser
```

### 2.4 `usermod`
- কাজ: ইউজারের সেটিংস পরিবর্তন করে

উদাহরণ:
```bash
sudo usermod -aG sudo newuser
```
ব্রেকডাউন:
- `-aG` : গ্রুপে যোগ করবে
- `sudo` : গ্রুপের নাম
- `newuser` : টার্গেট ইউজার

### 2.5 `deluser`
- কাজ: ইউজার মুছে ফেলে

উদাহরণ:
```bash
sudo deluser --remove-home olduser
```
- `--remove-home` : হোম ডিরেক্টরি ও ফাইল সহ মুছবে

### 2.6 `su`
- পূর্ণ রূপ: substitute user বা switch user
- কাজ: অন্য ইউজারে স্যুইচ করে

উদাহরণ:
```bash
su -
```
- `-` : সেল পরিবেশ গ্রহণ করে সে ইউজারের ডিফল্ট শেল

### 2.7 `sudo`
- পূর্ণ রূপ: superuser do
- কাজ: প্রশাসনিক অধিকার দিয়ে কমান্ড চালায়

উদাহরণ:
```bash
sudo visudo
```
- `visudo` : সেফলি `/etc/sudoers` ফাইল এডিট করে

---

## 3. নেটওয়ার্ক কনফিগারেশন

### 3.1 `ip addr show`
- `ip` : নেটওয়ার্ক কনফিগারেশন টুল
- `addr` : IP ঠিকানা সম্পর্কিত তথ্য
- `show` : দেখাও

উদাহরণ:
```bash
ip addr show
```

### 3.2 `ip link set`
- কাজ: ইন্টারফেস চালু বা বন্ধ করে

উদাহরণ:
```bash
sudo ip link set eth0 up
sudo ip link set eth0 down
```

### 3.3 `nmcli`
- পূর্ণ রূপ: NetworkManager command line interface
- কাজ: নেটওয়ার্ক প্রোফাইল দেখায়, তৈরি করে, সক্রিয় করে

উদাহরণ:
```bash
nmcli connection show
nmcli device status
```

### 3.4 `ping`
- কাজ: অন্য হোস্টে পৌঁছাচ্ছে কিনা পরীক্ষা করে

উদাহরণ:
```bash
ping -c 4 8.8.8.8
```
- `-c 4` : ৪ টি প্যাকেট পাঠাবে

### 3.5 `traceroute`
- কাজ: প্যাকেট কোন রাউটার পেরিয়ে যাবে দেখায়

উদাহরণ:
```bash
sudo traceroute google.com
```

### 3.6 `ss`
- কাজ: সকেট সংযোগ দেখায়

উদাহরণ:
```bash
ss -tuln
```
ব্রেকডাউন:
- `-t` : TCP
- `-u` : UDP
- `-l` : লিসেনিং সকেট
- `-n` : নম্বর দেখাবে, নাম নয়

### 3.7 `route`
- কাজ: রাউটিং টেবিল দেখায়

উদাহরণ:
```bash
ip route show
```

### 3.8 `hostnamectl`
- কাজ: সিস্টেম হোস্টনেম ও মেটাডেটা দেখায়/সেট করে

উদাহরণ:
```bash
hostnamectl status
sudo hostnamectl set-hostname myserver
```

---

## 4. গুরুত্বপূর্ণ কমান্ড ও লাইন

### 4.1 ডিস্ক এবং মাউন্ট

`df -h`
- `df` : disk filesystem
- `-h` : মানব-পঠিত মাপ

`du -sh /path`
- `du` : disk usage
- `-s` : সামারি
- `-h` : মানুষের পঠনযোগ্য

`mount | grep /dev/sda1`
- `mount` : মাউন্টকৃত ফাইল সিস্টেম দেখায়
- `|` : আউটপুট সরাসরি `grep` এ পাঠায়
- `grep /dev/sda1` : নির্দিষ্ট ডিভাইস খোঁজে

### 4.2 সিস্টেম লোগ

`journalctl -xe`
- `journalctl` : সিস্টেমলগ দেখা
- `-x` : ব্যাখ্যা সহ দেখান
- `-e` : শেষ অংশে যান

`sudo journalctl -u apache2.service --since "1 hour ago"`
- `-u apache2.service` : নির্দিষ্ট সার্ভিস
- `--since` : সময় সীমা

### 4.3 সার্ভিস ম্যানেজমেন্ট

`systemctl status nginx.service`
- `systemctl` : সিস্টেম সার্ভিস ম্যানেজার
- `status` : অবস্থা দেখায়
- `nginx.service` : টার্গেট সার্ভিস

`sudo systemctl restart networking`
- `restart` : সার্ভিস রিস্টার্ট
- `networking` : সার্ভিসের নাম

`sudo systemctl enable docker`
- `enable` : সিস্টেম বুটে চালু হবে

### 4.4 রুট access / root shell

`sudo -i`
- `-i` : ইনটারঅ্যাক্টিভ শেল, রুটের পরিবেশ নেয়

`sudo -s`
- `-s` : শেল সেন্ড, বর্তমান পরিবেশ ধরে

`sudo su -`
- `sudo` : প্রশাসনিক অধিকার
- `su -` : রুটে স্যুইচ করে পূর্ণ পরিবেশ নিয়ে

---

## 5. "বড় লাইন" কমান্ড উদাহরণ ও ব্যাখ্যা

### 5.1 ফাইল পারমিশন ও মালিক পরিবর্তন এক সঙ্গে

```bash
sudo chown -R user:group /var/www && sudo chmod -R 755 /var/www
```
ব্রেকডাউন:
- `sudo` : প্রশাসনিক অধিকার দরকার
- `chown` : মালিক পরিবর্তন
- `-R` : রিকারসিভভাবে সমস্ত ভেতরের ফাইল ও ফোল্ডার
- `user:group` : নতুন মালিক ও গ্রুপ
- `/var/www` : টার্গেট
- `&&` : প্রথম কমান্ড সাফল্য করলে দ্বিতীয় চালাবে
- `chmod -R 755 /var/www` : পারমিশন সেট করবে

### 5.2 নির্দিষ্ট শেল ফাইল খোঁজা

```bash
sudo find / -type f -perm /111 -name "*.sh" 2>/dev/null
```
ব্রেকডাউন:
- `find /` : রুট থেকে অনুসন্ধান শুরু
- `-type f` : শুধুমাত্র ফাইল
- `-perm /111` : executable পোরমিশন যেকোন গ্রুপে
- `-name "*.sh"` : নাম `.sh` দিয়ে শেষ হওয়া
- `2>/dev/null` : ত্রুটি মেসেজগুলো বাদ দাও

### 5.3 নেটওয়ার্ক ইন্টারফেসে আইপি দেখানো

```bash
ip addr show eth0 | grep "inet "
```
ব্রেকডাউন:
- `ip addr show eth0` : eth0 ইন্টারফেসের আইপি তথ্য
- `|` : পাইপ, আউটপুট অন্য কমান্ডে পাঠায়
- `grep "inet "` : শুধুমাত্র `inet` লাইন দেখায় (IPv4 ঠিকানা)

### 5.4 `sed` দিয়ে টেক্সট রিপ্লেস

```bash
sudo sed -i 's/old.example.com/new.example.com/g' /etc/hosts
```
ব্রেকডাউন:
- `sudo` : প্রশাসনিক অধিকার, কারণ `/etc/hosts` রুট-রাইটেবল
- `sed` : স্ট্রিম এডিটর
- `-i` : ফাইলের মধ্যে সরাসরি পরিবর্তন
- `'s/old.example.com/new.example.com/g'` : প্রতিস্থাপন প্যাটার্ন
- `/etc/hosts` : লক্ষ্য ফাইল

### 5.5 লোগও দেখার জন্য পাইপ ব্যবহার

```bash
sudo journalctl -u ssh.service -n 50 | tail -n 20
```
ব্রেকডাউন:
- `journalctl -u ssh.service` : ssh সার্ভিসের লোগ
- `-n 50` : শেষ ৫০ লাইন
- `|` : আউটপুট `tail` এ পাঠায়
- `tail -n 20` : শেষ ২০ লাইন দেখায়

---

## 6. গুরুত্বপূর্ণ নোট

- `sudo` ছাড়া অনেক প্রশাসনিক কমান্ড কাজ করবে না।
- `rm -rf` খুব সাবধানতার সঙ্গে ব্যবহার করুন; এটি ডেটা স্থায়ীভাবে মুছতে পারে।
- `chmod 777` সাধারণত নিরাপদ নয়, কারণ এটি সবার জন্য লেখার অনুমতি দেয়।
- নেটওয়ার্ক পরিবর্তন করার আগে বর্তমান কনফিগারেশন ব্যাকআপ রাখা ভালো।
- `visudo` ব্যবহার করুন `/etc/sudoers` এডিট করার জন্য; এটি সিনট্যাক্স চেক করে, ভুল হলে সিস্টেম লক হওয়া রোধ করে।

## 7. আরো গুরুত্বপূর্ণ Ubuntu কমান্ড

### 7.1 প্রক্রিয়া ও সিস্টেম মনিটর

`ps aux`
- `ps` : process status
- `a` : সব ব্যবহারকারীর প্রক্রিয়া
- `u` : ইউজার-ফরম্যাট
- `x` : টার্মিনাল ছাড়া প্রক্রিয়াও দেখাও

উদাহরণ:
```bash
ps aux | grep apache2
```
- `grep apache2` দিয়ে Apache প্রক্রিয়া খোঁজা হচ্ছে

`top`
- রিয়েল-টাইম CPU ও মেমরি ব্যবহার দেখায়
- `q` চাপলে বের হওয়া যায়

উদাহরণ:
```bash
top
```

`htop`
- `top`-এর উন্নত ভার্সন (আগে ইনস্টল করতে হতে পারে)
- গ্রাফিকাল ইন্টারফেসে প্রক্রিয়া দেখায়

উদাহরণ:
```bash
sudo apt install htop
htop
```

`kill PID`
- একটি নির্দিষ্ট PID কে বন্ধ করে

উদাহরণ:
```bash
kill 3456
```
- PID 3456 প্রক্রিয়া বন্ধ করবে

`killall process_name`
- ওই নামের সব প্রক্রিয়া বন্ধ করে

উদাহরণ:
```bash
sudo killall nginx
```

`nice -n 10 command`
- কমান্ডের প্রায়োরিটি কমিয়ে দেয়

উদাহরণ:
```bash
nice -n 10 rsync -av /source/ /dest/
```

`renice -n 5 -p 1234`
- চলমান প্রক্রিয়ার প্রায়োরিটি পরিবর্তন করে

উদাহরণ:
```bash
sudo renice -n 5 -p 1234
```

### 7.2 সিস্টেম তথ্য

`uname -a`
- লিনাক্স কার্নেল ও সিস্টেম তথ্য দেখায়

উদাহরণ:
```bash
uname -a
```

`lscpu`
- CPU আর্কিটেকচার সম্পর্কিত তথ্য

উদাহরণ:
```bash
lscpu | grep 'Model name'
```

`free -h`
- র‍্যাম ও সুয়াপ ব্যবহার দেখায়

উদাহরণ:
```bash
free -h
```

`uptime`
- সিস্টেম কতক্ষণ চালু আছে দেখায়

উদাহরণ:
```bash
uptime
```

`who`
- বর্তমানে কোন ব্যবহারকারী লগইন করেছে

উদাহরণ:
```bash
who
```

`last -n 10`
- শেষ ১০টি লগইন অ্যাক্টিভিটি দেখায়

উদাহরণ:
```bash
last -n 10
```

### 7.3 ফাইল অনুসন্ধান ও পার্থক্য

`find /home -name "*.log"`
- নির্দিষ্ট ডিরেক্টরিতে ফাইল খুঁজে

উদাহরণ:
```bash
find /var/log -name "*.log"
```

`locate syslog`
- দ্রুত খোঁজার জন্য ট্রান্সলেটেড ডাটাবেস ব্যবহার
- প্রথমে `sudo updatedb` করতে হতে পারে

উদাহরণ:
```bash
sudo updatedb
locate syslog
```

`diff file1.txt file2.txt`
- দুইটি ফাইলের পরিবর্তন দেখায়

উদাহরণ:
```bash
diff /etc/hosts /tmp/hosts.backup
```

`cmp file1.bin file2.bin`
- বাইনারি ফাইলের প্রথম পার্থক্য দেখায়

উদাহরণ:
```bash
cmp /usr/bin/python3 /tmp/python3_copy
```

### 7.4 আর্কাইভ ও কম্প্রেশন

`tar -czvf backup.tar.gz /home/user/project`
- `-c` : আর্কাইভ তৈরি
- `-z` : gzip কম্প্রেশন
- `-v` : ভেবোসলি আউটপুট দেখাও
- `-f` : ফাইল নাম নির্দিষ্ট

উদাহরণ:
```bash
tar -czvf project_backup.tar.gz /home/user/project
```

`tar -xzvf backup.tar.gz`
- `.tar.gz` আর্কাইভ এক্সট্র্যাক্ট করে

উদাহরণ:
```bash
tar -xzvf project_backup.tar.gz
```

`zip -r project.zip project/`
- ফোল্ডার জিপ ফাইল তৈরি করে

উদাহরণ:
```bash
zip -r project.zip project/
```

`unzip project.zip`
- জিপ ফাইল এক্সট্র্যাক্ট করে

উদাহরণ:
```bash
unzip project.zip
```

### 7.5 নেটওয়ার্ক টেস্ট ও ট্রাবলশুট

`curl -I https://example.com`
- `-I` : শুধুমাত্র HTTP হেডার দেখায়

উদাহরণ:
```bash
curl -I https://example.com
```

`wget https://example.com/file.tar.gz`
- ফাইল ডাউনলোড করে

উদাহরণ:
```bash
wget https://example.com/file.tar.gz
```

`dig example.com`
- DNS তথ্য অনুসন্ধান করে

উদাহরণ:
```bash
dig example.com
```

`nslookup example.com`
- DNS রেকর্ড দেখতে ব্যবহৃত

উদাহরণ:
```bash
nslookup example.com
```

`tcpdump -i eth0 port 80`
- `eth0` ইন্টারফেসে HTTP প্যাকেট ক্যাপচার করে

উদাহরণ:
```bash
sudo tcpdump -i eth0 port 80
```

### 7.6 ফাইল ও ডিরেক্টরি ব্যাকআপ ও কপি

`rsync -av --delete /source/ /dest/`
- `-a` : আর্কাইভ মোড
- `-v` : ভেবোসলি
- `--delete` : গন্তব্যে অনুপস্থিত ফাইল মুছবে

উদাহরণ:
```bash
rsync -av --delete /home/user/project/ /backup/project/
```

`cp -a /etc /backup/etc`
- `-a` : আর্কাইভ, সকল অ্যাট্রিবিউট রেখে কপি

উদাহরণ:
```bash
cp -a /etc /backup/etc
```

### 7.7 ক্রন জব ও শিডিউল

`crontab -e`
- বর্তমান ব্যবহারকারীর ক্রন টাস্ক এডিট করে

উদাহরণ:
```bash
crontab -e
```

`crontab -l`
- বর্তমান ক্রন অন্তর তালিকা দেখায়

উদাহরণ:
```bash
crontab -l
```

গ্রাহক:
```cron
0 2 * * * /usr/bin/backup.sh
```
- প্রথম পাঁচটি ফিল্ড: মিনিট, ঘণ্টা, দিন, মাস, সাপ্তাহিক দিন
- এরপর কমান্ড

### 7.8 শেল টিপস

`history | grep apt`
- পূর্বের কমান্ডের মধ্যে `apt` খোঁজে

উদাহরণ:
```bash
history | grep apt
```

`!!`
- আগের কমান্ড পুনরায় চালায়

উদাহরণ:
```bash
sudo apt update
!!
```

`!$`
- আগের কমান্ডের শেষ আর্গুমেন্ট ব্যবহার করে

উদাহরণ:
```bash
echo hello
cat !$
```

`alias ll='ls -lah'`
- শর্টকাট তৈরি করে

উদাহরণ:
```bash
alias ll='ls -lah'
ll
```

`unalias ll`
- একটি আলিয়াস মুছে দেয়

উদাহরণ:
```bash
unalias ll
```

### 7.9 নিরাপত্তা ও ফায়ারওয়াল

`ufw status verbose`
- UFW ফায়ারওয়ালের অবস্থা দেখায়

উদাহরণ:
```bash
sudo ufw status verbose
```

`sudo ufw allow 22/tcp`
- SSH পোর্ট অনুমোদন করে

উদাহরণ:
```bash
sudo ufw allow 22/tcp
```

`sudo ufw deny 23/tcp`
- Telnet পোর্ট ব্লক করে

উদাহরণ:
```bash
sudo ufw deny 23/tcp
```

`sudo ufw enable`
- ফায়ারওয়াল চালু করে

উদাহরণ:
```bash
sudo ufw enable
```

### 7.10 অন্যান্য দরকারি কমান্ড

`sudo apt update && sudo apt upgrade`
- প্যাকেজ তালিকা আপডেট করে, তারপর প্যাকেজ আপগ্রেড করে

উদাহরণ:
```bash
sudo apt update && sudo apt upgrade -y
```

`sudo apt install htop tree vim`
- একবাত্রে একাধিক প্যাকেজ ইনস্টল করে

উদাহরণ:
```bash
sudo apt install htop tree vim
```

`tree -L 2`
- ডিরেক্টরির গাছ দেখায় দুই লেভেল পর্যন্ত

উদাহরণ:
```bash
tree -L 2
```

`watch -n 2 df -h`
- প্রতি ২ সেকেন্ডে `df -h` চালায়

উদাহরণ:
```bash
watch -n 2 df -h
```
## 8. উপসংহার
এই ফাইলে ফাইল এক্সেস, ইউজার ও রুট ম্যানেজমেন্ট, নেটওয়ার্ক কনফিগারেশন, মনিটরিং, ব্যাকআপ ও আরও অনেক গুরুত্বপূর্ণ Ubuntu কমান্ড ব্যাখ্যা করা হয়েছে। এগুলো দিয়ে আরও শক্তিশালীভাবে সিস্টেম পরিচালনা করতে পারবেন।
