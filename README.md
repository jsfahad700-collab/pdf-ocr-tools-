# Voter ZIP PDF Extractor — Termux ব্যবহার নির্দেশিকা

বাংলা ভোটার PDF-যুক্ত `voters.zip` ফাইল থেকে `voters.json` তৈরি করার Python টুল। Android ফোনের Termux থেকেই চালানো যাবে। কম্পিউটারের প্রয়োজন নেই।

## ধাপ ১: প্রয়োজনীয় অ্যাপ ইনস্টল করুন

Android ফোনে Termux ইনস্টল করুন। বিশ্বস্ত ও আপডেটেড Termux বিল্ড ব্যবহার করুন।

## ধাপ ২: ফোনে ZIP ফাইল রাখুন

ফোনের Internal Storage-এ `Votar` নামে একটি ফোল্ডার তৈরি করুন।

তারপর মূল ZIP ফাইলটি ওই ফোল্ডারে রাখুন এবং ফাইলটির নাম দিন:

`voters.zip`

ফোল্ডারটি এমন হবে:

```text
Internal storage/
└── Votar/
    └── voters.zip
```

## ধাপ ৩: Termux প্রস্তুত করুন

Termux খুলে নিচের কমান্ডগুলো একে একে চালান।

প্রথমে Storage Permission দিন:

```bash
termux-setup-storage
```

Android ফোনে Permission চাইলে **Allow** চাপুন।

এরপর Termux আপডেট করুন:

```bash
pkg update && pkg upgrade -y
```

প্রয়োজনীয় প্যাকেজ ইনস্টল করুন:

```bash
pkg install python git unzip -y
```

## ধাপ ৪: GitHub থেকে কোড ডাউনলোড করুন

নিচের কমান্ড দিয়ে Repository Clone করুন:

```bash
cd ~
git clone https://github.com/jsfahad700-collab/pdf-ocr-tools-.git
```

এরপর প্রজেক্ট ফোল্ডারে প্রবেশ করুন:

```bash
cd ~/pdf-ocr-tools-
```

**যদি আগে থেকেই Repository ডাউনলোড করা থাকে**, তাহলে আবার `git clone` করবেন না। শুধু এই কমান্ড চালান:

```bash
cd ~/pdf-ocr-tools-
```

## ধাপ ৫: Python লাইব্রেরি ইনস্টল করুন

প্রজেক্ট ফোল্ডারের ভিতরে থেকে চালান:

```bash
python -m pip install -r requirements.txt
```

ইনস্টল শেষ হওয়া পর্যন্ত অপেক্ষা করুন।

মনে রাখবেন: প্রতিবার চালানোর সময় লাইব্রেরি আবার ইনস্টল করার প্রয়োজন নেই।

## ধাপ ৬: ZIP ফাইল আছে কি না পরীক্ষা করুন

চালান:

```bash
ls -lh ~/storage/shared/Votar/voters.zip
```

ফাইল দেখা গেলে বুঝবেন ZIP ফাইল ঠিক জায়গায় আছে।

ফাইল না দেখালে File Manager-এ গিয়ে `Internal storage/Votar/` ফোল্ডার এবং Termux-এর Storage Permission পরীক্ষা করুন।

## ধাপ ৭: স্ক্রিপ্ট চালু করুন

এখন এই কমান্ডটি চালান:

```bash
python voter_extractor.py
```

স্ক্রিপ্ট চালু হলে কাজ শেষ হওয়া পর্যন্ত অপেক্ষা করুন।

## ধাপ ৮: ফলাফল দেখুন

কাজ শেষ হলে সাধারণত `Internal storage/Votar/` ফোল্ডারে ফলাফল পাবেন:

```text
Votar/
├── voters.zip
├── voters.json
├── suspect_report.txt
└── unknown_glyphs.png
```

ফাইলগুলোর কাজ:

- `voters.json` — PDF থেকে পাওয়া রেকর্ড।
- `suspect_report.txt` — সন্দেহজনক বা অজানা লেখার রিপোর্ট।
- `unknown_glyphs.png` — তৈরি হলে অজানা অক্ষরের ছবি।

## ধাপ ৯: পরের বার চালানোর নিয়ম

একবার সেটআপ ও লাইব্রেরি ইনস্টল হয়ে গেলে পরের বার শুধু Termux খুলে এই দুটি কমান্ড চালালেই হবে:

```bash
cd ~/pdf-ocr-tools-
python voter_extractor.py
```

ব্যস! স্ক্রিপ্ট আবার চালু হয়ে যাবে।

## সমস্যা হলে করণীয়

**১. voters.zip পাওয়া যাচ্ছে না**

```bash
termux-setup-storage
ls -lh ~/storage/shared/Votar/
```

**২. Python Module পাওয়া যাচ্ছে না**

```bash
cd ~/pdf-ocr-tools-
python -m pip install -r requirements.txt
```

**৩. Repository আগে থেকেই আছে**

আবার Clone করবেন না। চালান:

```bash
cd ~/pdf-ocr-tools-
```

**৪. স্ক্রিপ্ট চালু হচ্ছে না**

```bash
cd ~/pdf-ocr-tools-
python voter_extractor.py
```

এরপর Termux-এ দেখানো সম্পূর্ণ Error Message কপি করে সহায়তা নিন।

## Privacy ও নিরাপত্তা

- আসল `voters.zip` এবং তৈরি হওয়া `voters.json` Public GitHub-এ আপলোড করবেন না।
- ব্যক্তিগত ভোটার ডাটা নিজের ফোনে সংরক্ষণ করুন।
- ডাটা ব্যবহারের ক্ষেত্রে প্রযোজ্য আইন ও অনুমতি মেনে চলুন।

---

**GitHub Repository:**

https://github.com/jsfahad700-collab/pdf-ocr-tools-

**Run Command:**

```bash
cd ~/pdf-ocr-tools- && python voter_extractor.py
```