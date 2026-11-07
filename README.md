# Voter ZIP PDF Extractor — Termux

বাংলা ভোটার PDF-যুক্ত `voters.zip` থেকে `voters.json` তৈরি করার Termux-উপযোগী Python স্ক্রিপ্ট। Android ফোনেই চালানো যাবে; কম্পিউটার প্রয়োজন নেই।

> **প্রয়োজন:** Android-এ Termux ইনস্টল থাকতে হবে। Termux-এর আপডেটেড/বিশ্বস্ত বিল্ড ব্যবহার করুন।

## 1. ফোনে ZIP ফাইল রাখুন

File Manager দিয়ে Internal Storage-এ `Votar` নামে ফোল্ডার তৈরি করুন এবং আপনার মূল ZIP ফাইলটির নাম হুবহু `voters.zip` রাখুন।

```text
Internal storage/
└── Votar/
    └── voters.zip
```

Termux-এ storage permission দেওয়ার পর স্ক্রিপ্ট নিজে থেকেই এই ফোল্ডার খুঁজবে। ZIP-এর পাশেই ফলাফল তৈরি হবে।

## 2. Termux প্রথমবার প্রস্তুত করুন

Termux খুলে নিচের কমান্ডগুলো একে একে চালান। Storage permission চাইলে Android-এর Allow দিন।

```bash
termux-setup-storage
pkg update && pkg upgrade -y
pkg install python git unzip -y
```

Shared storage দেখা যাচ্ছে কি না পরীক্ষা করুন:

```bash
ls -la ~/storage/shared/Votar
```

যদি `voters.zip` দেখা যায়, ফোল্ডার ঠিক আছে। না দেখালে File Manager-এ `Internal storage/Votar/voters.zip` আছে কি না এবং Termux-এর Files permission চালু আছে কি না পরীক্ষা করুন।

## 3. GitHub থেকে Repository Clone করুন (প্রস্তাবিত)

GitHub-এ আপনার repository তৈরি করে এই কোডগুলো সেখানে আপলোড করুন। তারপর নিচে `YOUR_USERNAME` ও `YOUR_REPO`-এর জায়গায় নিজের GitHub username এবং repository name বসান।

```bash
cd ~
git clone https://github.com/jsfahad700-collab/pdf-ocr-tools-.git
cd pdf-ocr-tools-
```

উদাহরণ: username `forhad123` এবং repository `Voter-Extractor` হলে:

```bash
cd ~
git clone https://github.com/jsfahad700-collab/pdf-ocr-tools-.git
cd pdf-ocr-tools-
```

**যদি GitHub থেকে ZIP ফাইল ডাউনলোড করেন (Clone নয়):** ZIP সাধারণত Download ফোল্ডারে থাকবে।

```bash
cd ~/storage/downloads
ls
unzip Voter-Extractor-Termux.zip -d ~/Voter-Extractor
cd ~/Voter-Extractor/Voter-Extractor-Termux
```

ডাউনলোড করা ZIP-এর নাম আলাদা হলে `unzip` কমান্ডে সেই সঠিক নাম দিন। ZIP-এর ভিতরের ফোল্ডারের নাম ভিন্ন হলে `ls` দিয়ে দেখে সেই ফোল্ডারে ঢুকুন।

## 4. Python লাইব্রেরি ইনস্টল করুন

Repository/স্ক্রিপ্ট ফোল্ডারের ভিতরে থেকে চালান:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## 5. স্ক্রিপ্ট চালান

```bash
python voter_extractor.py
```

স্ক্রিপ্ট `/storage/emulated/0/Votar`, `/sdcard/Votar` এবং Termux shared storage-এর `Votar` ফোল্ডারসহ নির্ধারিত জায়গাগুলোতে `voters.zip` খুঁজবে।

## 6. ফলাফল কোথায় পাবেন

কাজ শেষ হলে সাধারণত `Internal storage/Votar/` ফোল্ডারে পাবেন:

```text
Votar/
├── voters.zip
├── voters.json
├── suspect_report.txt
└── unknown_glyphs.png   (প্রয়োজন হলে তৈরি হবে)
```

- `voters.json` — ZIP-এর PDF থেকে পাওয়া একত্রিত রেকর্ড।
- `suspect_report.txt` — সন্দেহজনক/অজানা লেখা ও অক্ষরের রিপোর্ট।
- `unknown_glyphs.png` — অজানা অক্ষরের ছবি তৈরি হলে।

## 7. পরের বার চালানোর কমান্ড

Termux বন্ধ করে আবার খুললে শুধু এই কমান্ডগুলো যথেষ্ট (আপনার clone করা ফোল্ডারের নাম অনুযায়ী `cd` ঠিক করুন):

```bash
cd ~/YOUR_REPO
python voter_extractor.py
```

লাইব্রেরি একবার ইনস্টল হয়ে গেলে প্রতিবার আবার ইনস্টল করতে হবে না।

## 8. GitHub-এ কোড আপলোড করার কমান্ড (ঐচ্ছিক)

প্রথমে GitHub ওয়েবসাইটে একটি **খালি repository** তৈরি করুন। তারপর Termux-এ এই প্রজেক্ট ফোল্ডারে গিয়ে `YOUR_USERNAME` ও `YOUR_REPO` বদলে চালান:

```bash
cd ~/Voter-Extractor-Termux
git init
git add voter_extractor.py requirements.txt README.md LICENSE .gitignore
git commit -m "Add Termux voter ZIP extractor"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

GitHub authentication চাইলে GitHub-এর অনুমোদিত sign-in/token পদ্ধতি ব্যবহার করুন। Password সরাসরি কমান্ডে লিখবেন না। যদি repository-তে আগে থেকেই ফাইল থাকে, আগে GitHub-এর সঙ্গে পরিবর্তন মিলিয়ে নিন; অন্ধভাবে force push করবেন না।

## 9. সমস্যা সমাধান

**`voters.zip` খুঁজে পাচ্ছে না:**

```bash
termux-setup-storage
ls -lh ~/storage/shared/Votar/voters.zip
ls -lh /storage/emulated/0/Votar/voters.zip
```

ফাইলের নাম `voters.zip` কি না নিশ্চিত করুন। Android Settings থেকে Termux-এর Files/Storage permission Allow করুন।

**কোনো Python module নেই:**

```bash
cd ~/YOUR_REPO
python -m pip install -r requirements.txt
```

**ফোন গরম বা ধীর হলে:** স্ক্রিপ্টের সেটিংসে `WORKERS`-এর মান `1` বা `2` করুন। এতে প্রসেসিং ধীর হতে পারে, তবে একসঙ্গে কম PDF প্রসেস হবে।

**লগ/ত্রুটি দেখতে:** Termux-এ স্ক্রিপ্ট চালানোর সময় যে লেখা দেখায় তা দেখে নিন; প্রয়োজন হলে পুরো error message কপি করে সহায়তা নিন।

## Privacy ও ডাটা সুরক্ষা

আসল `voters.zip`, তৈরি হওয়া `voters.json` এবং ব্যক্তিগত ভোটার ডাটা কখনো Public GitHub repository-তে commit বা push করবেন না। `.gitignore`-এ এসব ফাইল বাদ দেওয়া আছে, তবুও `git status` দেখে নিশ্চিত হোন। ডাটা নিজের ফোনে রাখুন এবং ব্যবহারের ক্ষেত্রে প্রযোজ্য আইন ও অনুমতি মেনে চলুন।
