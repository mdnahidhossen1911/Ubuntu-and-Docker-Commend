# Ubuntu Command Guide (বাংলা)

## 1. পরিচিতি
Ubuntu হচ্ছে লিনাক্স ভিত্তিক অপারেটিং সিস্টেম। টার্মিনাল এমন একটি জায়গা যেখানে আপনি Text commands দিয়ে কাজ করেন। এখানে সাধারণ থেকে উন্নত কমান্ডগুলোর ব্যাখ্যা দেওয়া হয়েছে।

## 2. বেসিক কমান্ড

### 2.1 `pwd`
- পূর্ণ রূপ: print working directory
- কাজ: বর্তমান ডিরেক্টরির পথ দেখায়।
- ব্যবহার:
  ```bash
  pwd
  ```

### 2.2 `ls`
- পূর্ণ রূপ: list
- কাজ: ডিরেক্টরির ফাইল ও ফোল্ডার দেখায়।
- সাধারণ ব্যবহার:
  ```bash
  ls
  ```
- অপশন:
  - `-l` : বিস্তারিত তালিকা
  - `-a` : লুকানো ফাইল দেখায়
  - `-h` : মানুষের পঠিত ফাইল সাইজ
  ```bash
  ls -lah
  ```

### 2.3 `cd`
- পূর্ণ রূপ: change directory
- কাজ: ডিরেক্টরি পরিবর্তন করে।
- ব্যবহার:
  ```bash
  cd /home/username/Documents
  cd ..        # উপরের ডিরেক্টরিতে ওঠা
  cd ~         # হোম ডিরেক্টরিতে যাওয়া
  ```

### 2.4 `mkdir`
- পূর্ণ রূপ: make directory
- কাজ: নতুন ফোল্ডার তৈরি করে।
- ব্যবহার:
  ```bash
  mkdir my_folder
  mkdir -p a/b/c   # nested ডিরেক্টরি তৈরি
  ```

### 2.5 `rm`
- পূর্ণ রূপ: remove
- কাজ: ফাইল বা ফোল্ডার মোছা।
- সতর্কতা: `rm` ফাইল স্থায়ীভাবে মুছে দেয়।
- ব্যবহার:
  ```bash
  rm file.txt
  rm -r folder/   # ফোল্ডার সহ ভিতরের সব কিছু মোছা
  rm -f file.txt  # জোরপূর্বক মোছানো
  ```

### 2.6 `cp`
- পূর্ণ রূপ: copy
- কাজ: ফাইল বা ফোল্ডার কপি করে।
- ব্যবহার:
  ```bash
  cp source.txt destination.txt
  cp -r folder1 folder2
  ```

### 2.7 `mv`
- পূর্ণ রূপ: move
- কাজ: ফাইল/ফোল্ডার স্থানান্তর বা রিনেম করা।
- ব্যবহার:
  ```bash
  mv oldname.txt newname.txt
  mv file.txt /home/username/Documents/
  ```

## 3. ইন্সটলেশন ও প্যাকেজ ম্যানেজমেন্ট

### 3.1 `sudo`
- পূর্ণ রূপ: superuser do
- কাজ: প্রশাসনিক অধিকার দিয়ে কমান্ড চালায়।
- ব্যবহার:
  ```bash
  sudo apt update
  ```

### 3.2 `apt`
- পূর্ণ রূপ: Advanced Package Tool
- কাজ: সফটওয়্যার প্যাকেজ ইনস্টল, আপডেট, রিমুভ করা।
- সাধারণ কমান্ড:
  ```bash
  sudo apt update          # প্যাকেজ তালিকা আপডেট
  sudo apt upgrade         # ইনস্টল করা প্যাকেজ আপডেট
  sudo apt install git     # git ইনস্টল
  sudo apt remove nano     # nano মোছা
  ```

### 3.3 `apt-cache`
- কাজ: প্যাকেজ তথ্য খোঁজার জন্য।
- ব্যবহার:
  ```bash
  apt-cache search firefox
  apt-cache show vim
  ```

## 4. ফাইল ও টেক্সট সংক্রান্ত কমান্ড

### 4.1 `cat`
- পূর্ণ রূপ: concatenate
- কাজ: ফাইলের কন্টেন্ট দেখায় বা একাধিক ফাইল যোগ করে।
- ব্যবহার:
  ```bash
  cat file.txt
  cat file1.txt file2.txt
  ```

### 4.2 `less`
- কাজ: বড় ফাইল ধাপে ধাপে দেখায়।
- ব্যবহার:
  ```bash
  less file.txt
  ```
- কী বোর্ড: `q` দিয়ে বের হতে হবে।

### 4.3 `head` ও `tail`
- `head`: প্রথম ১০ লাইন দেখায়
- `tail`: শেষ ১০ লাইন দেখায়
- ব্যবহার:
  ```bash
  head -n 5 file.txt
  tail -n 20 file.txt
  ```

### 4.4 `grep`
- পূর্ণ রূপ: global regular expression print
- কাজ: টেক্সটে শব্দ বা প্যাটার্ন খোঁজে।
- ব্যবহার:
  ```bash
  grep "hello" file.txt
  grep -r "TODO" ./project
  ```

### 4.5 `find`
- কাজ: ফাইল বা ডিরেক্টরি অনুসন্ধান করে।
- ব্যবহার:
  ```bash
  find . -name "*.py"
  find /home -type f -size +10M
  ```

## 5. সিস্টেম ও নেটওয়ার্ক

### 5.1 `top`
- কাজ: চলমান প্রক্রিয়ার তালিকা দেখায়।
- ব্যবহার:
  ```bash
  top
  ```
- `q` প্রেস করলে বের হওয়া যায়।

### 5.2 `ps`
- পূর্ণ রূপ: process status
- কাজ: প্রক্রিয়া বস্তু দেখায়।
- ব্যবহার:
  ```bash
  ps aux | grep firefox
  ```

### 5.3 `df`
- পূর্ণ রূপ: disk filesystem
- কাজ: ডিস্ক ব্যবহার দেখায়।
- ব্যবহার:
  ```bash
  df -h
  ```

### 5.4 `du`
- পূর্ণ রূপ: disk usage
- কাজ: ফাইল বা ফোল্ডারের জায়গা দেখায়।
- ব্যবহার:
  ```bash
  du -sh /var/log
  ```

### 5.5 `chmod`
- পূর্ণ রূপ: change mode
- কাজ: ফাইল/ডিরেক্টরির পারমিশন বদলায়।
- ধারণা:
  - `r` = read, `w` = write, `x` = execute
  - `u` = user, `g` = group, `o` = others
- ব্যবহার:
  ```bash
  chmod u+rwx script.sh
  chmod 755 script.sh
  ```

### 5.6 `chown`
- পূর্ণ রূপ: change owner
- কাজ: মালিক বা গ্রুপ পরিবর্তন করে।
- ব্যবহার:
  ```bash
  sudo chown username:group file.txt
  ```

### 5.7 `ping`
- কাজ: নেটওয়ার্কে কোন হোস্টে পৌঁছানো যাচ্ছে কিনা পরীক্ষণ করে।
- ব্যবহার:
  ```bash
  ping google.com
  ```

### 5.8 `curl`
- কাজ: HTTP/HTTPS অনুরোধ পাঠায় এবং আউটপুট দেখায়।
- ব্যবহার:
  ```bash
  curl https://example.com
  ```

### 5.9 `shutdown` / power management
- কাজ: সিস্টেম বন্ধ, রিবুট বা শিডিউল করা। প্রশাসনিক (sudo) অধিকার লাগে।
- সাধারণ ব্যবহার:
  ```bash
  # এখনই শাটডাউন (power off)
  sudo shutdown -h now

  # এখনই রিবুট
  sudo shutdown -r now

  # নির্দিষ্ট সময় পরে শাটডাউন (উদাহরণ: 10 মিনিট পরে)
  sudo shutdown -P +10

  # দ্রুত পাওয়ার অফ / রিবুট
  sudo poweroff
  sudo reboot

  # systemd ব্যবহার করে
  sudo systemctl poweroff
  sudo systemctl reboot
  ```

সতর্কতা: শাটডাউন চালানোর আগে সব কাজ সংরক্ষণ করে নিন, কারণ চালু থাকা প্রক্রিয়া বন্ধ হয়ে যাবে।

### 5.10 Permanent removal / secure delete
- কাজ: ফাইল স্থায়ীভাবে মুছে ফেলা এবং সম্ভাব্যভাবে ডিস্কে থাকা ডেটা ওভাররাইট করা।
- সতর্কতা: SSD বা journaled ফাইল সিস্টেমে ভেরিফায়েবল ডিলিট করা কঠিন — সম্পূর্ণ ডিস্ক এনক্রিপশন ব্যবহার করাই সর্বোত্তম।
- সাধারণ টুল ও ব্যবহার:
  ```bash
  # GNU rm-এর কিছু সিস্টেমে -P (overwrite 3 times) অপশন থাকে
  rm -P secret.txt

  # shred: ফাইলকে ওভাররাইট করে, পরে মুছে ফেলে
  shred -u -v secret.txt

  # srm (secure-delete package) — ইন্সটল করে ব্যবহার করতে হয়
  srm -v secret.txt

  # যদি শুধু ওভাররাইট করে তারপর মুছতে চান (সাবধান):
  dd if=/dev/zero of=secret.txt bs=1M count=10 && rm secret.txt
  ```

- টিপস:
  - SSD-তে ডেটা পুরোপুরি অপসারণ নিশ্চিত নয় — ব্যবহার করুন full-disk encryption বা physically destroy if necessary.
  - প্যাকেজ ইন্সটল: `sudo apt install secure-delete` (srm) বা `sudo apt install coreutils` (shred/rm present)।

### 5.11 File location & memory / register position checks
- কাজ: ফাইলের inode, ব্লক/extent অবস্থান, এবং কোর মেমোরিতে (cache) আছে কিনা চেক করা।
- সাধারণ কমান্ড:
  ```bash
  # ফাইলের inode ও লিঙ্ক দেখার জন্য
  ls -li file.txt
  stat file.txt

  # ফাইল কোন ব্লকগুলোতে আছে (extent) দেখার জন্য
  filefrag -v file.txt

  # যদি অনুমতি থাকে, filesystem-level mapping দেখতে পারেন
  sudo hdparm --fibmap file.txt

  # কোন প্রসেস ফাইলটি খুলে রেখেছে দেখুন
  lsof -- file.txt

  # ফাইল বা পেজ cache(র্যাম) এ আছে কিনা পরীক্ষার জন্য (vmtouch ইনস্টল করে)
  vmtouch -v file.txt
  ```

- নোট: `filefrag` ও `--fibmap` ব্লক/extent তথ্য দেয়; কিন্তু SSD এবং LVM এর কারণে ফিজিক্যাল ব্লক নিশ্চিত না হতে পারে। `vmtouch` সব সিস্টেমে ইনস্টল নেই — `sudo apt install vmtouch` করে ব্যবহার করা যায়।

## 6. উন্নত কমান্ড

### 6.1 `tar`
- কাজ: ফাইল আর্কাইভ ও এক্সট্র্যাক্ট করে।
- ব্যবহার:
  ```bash
  tar -cvf archive.tar folder/
  tar -xvf archive.tar
  tar -czvf archive.tar.gz folder/
  tar -xzvf archive.tar.gz
  ```

### 6.2 `ssh`
- পূর্ণ রূপ: secure shell
- কাজ: রিমোট সার্ভারে লগইন করে।
- ব্যবহার:
  ```bash
  ssh user@server_ip
  ```

### 6.3 `scp`
- পূর্ণ রূপ: secure copy
- কাজ: রিমোট থেকে/রিমোটে ফাইল কপি করে।
- ব্যবহার:
  ```bash
  scp file.txt user@server:/path/
  scp user@server:/path/file.txt ./
  ```

### 6.4 `rsync`
- কাজ: ফাইল সিঙ্ক্রোনাইজ করে, দ্রুত আর নিরাপদ।
- ব্যবহার:
  ```bash
  rsync -avz source/ destination/
  ```

### 6.5 `sudo !!`
- কাজ: আগের কমান্ডটি প্রশাসনিক অধিকার দিয়ে আবার চালায়।
- ব্যবহার:
  ```bash
  sudo apt install git
  # যদি ভুল হয়:
  sudo !!
  ```

## 7. সাইন ও চিহ্নের ব্যাখ্যা

- `.` : বর্তমান ডিরেক্টরি
- `..` : উপরের ডিরেক্টরি
- `~` : হোম ডিরেক্টরি
- `|` : পাইপ, একটি কমান্ডের আউটপুট অন্য কমান্ডে পাঠায়
- `>` : আউটপুট ফাইলতে লেখে (ওভাররাইট)
- `>>` : আউটপুট ফাইলের শেষে যোগ করে
- `&` : ব্যাকগ্রাউন্ডে প্রক্রিয়া চালায়
- `*` : ওয়াইল্ডকার্ড, নামের যেকোন অংশ মানে

## 8. ব্যবহারিক উদাহরণ

- একটি ফাইলের প্রথম ২০ লাইন দেখার জন্য:
  ```bash
  head -n 20 file.txt
  ```
- `grep` দিয়ে লাইন খোঁজা:
  ```bash
  grep "error" /var/log/syslog
  ```
- একটি ডিরেক্টরির মধ্যে যত এসিএল দেখার জন্য:
  ```bash
  ls -lah
  ```
- ডিস্ক স্পেস দেখার জন্য:
  ```bash
  df -h
  ```

## 9. উপসংহার
এই ডকুমেন্টে বেসিক থেকে কিছু উন্নত Ubuntu কমান্ড ব্যাখ্যা করা হয়েছে। ধাপে ধাপে কমান্ড প্রয়োগ করে অনুশীলন করলে শিখতে সুবিধা হবে।
