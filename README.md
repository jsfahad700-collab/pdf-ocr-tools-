<div align="center">

# 🗳️ Voter Extractor

### বাংলা ভোটার PDF → `voters.json` 📄➡️🧾

Android ফোনের **Termux** দিয়েই চলবে 📱 — কম্পিউটার লাগবে না 💻❌

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Termux](https://img.shields.io/badge/Termux-Android-black?logo=android&logoColor=green)
![Output](https://img.shields.io/badge/Output-JSON-orange)

</div>

---

## ✨ এই টুল কী করে?

`voters.zip`-এর ভেতরের বাংলা ভোটার PDF পড়ে 📖 সব রেকর্ড একটি `voters.json` ফাইলে সাজিয়ে দেয় ✅

---

## ⚡ দ্রুত শুরু (শুধু কপি-পেস্ট)

> প্রথমবার সেটআপের জন্য Termux-এ নিচের **৩টি ব্লক** একটার পর একটা চালান 👇

**1️⃣ Storage Permission + প্যাকেজ ইনস্টল**

```bash
termux-setup-storage
pkg update -y && pkg upgrade -y
pkg install python git unzip -y
```

**2️⃣ কোড ডাউনলোড**

```bash
cd ~
git clone https://github.com/jsfahad700-collab/pdf-ocr-tools-.git
cd ~/pdf-ocr-tools-
```

**3️⃣ লাইব্রেরি ইনস্টল**

```bash
python -m pip install pypdf
python -m pip install rapidfuzz
```

> 💡 `rapidfuzz` ইনস্টল না হলেও সমস্যা নেই — টুল সেটা ছাড়াই চলবে।

---

## 📂 ZIP ফাইল কোথায় রাখবেন?

ফোনের Internal Storage-এ **Votar** নামে একটি ফোল্ডার বানান, তারপর ফাইলটি ওই ফোল্ডারে রাখুন এবং নাম দিন ঠিক:

```text
voters.zip
```

```text
📱 Internal storage/
└── 📁 Votar/
    └── 📦 voters.zip
```

ফাইল ঠিক জায়গায় আছে কি না দেখুন 🔍

```bash
ls -lh ~/storage/shared/Votar/voters.zip
```

ফাইলের নাম দেখালে ✅ ঠিক আছে। না দেখালে ❌ নিচের **সমস্যা সমাধান** অংশ দেখুন।

---

## ▶️ টুল চালান

```bash
cd ~/pdf-ocr-tools- && python voter_extractor.py
```

⏳ কাজ শেষ না হওয়া পর্যন্ত অপেক্ষা করুন। স্ক্রিন বন্ধ করবেন না এবং Termux ব্যাকগ্রাউন্ডে পাঠাবেন না।

> 🔋 **টিপস:** বড় ফাইল হলে চার্জে রাখুন এবং Termux খোলা রাখুন।
> 🔋 ব্যাটারি কম থাকলে বা Battery Saver চালু থাকলে ফোন CPU ধীর করে দেয় — দ্রুত চালাতে চার্জে রাখুন ও Battery Saver বন্ধ করুন।
> 🔥 ফোন বেশি গরম বা হ্যাং হলে `voter_extractor.py`-এর `WORKERS` সংখ্যা কমিয়ে `1` বা `2` দিন।

---

## 📊 লাইভ ড্যাশবোর্ড

চলার সময় Termux-এ একটি স্থির (স্ক্রিনে এক জায়গায় থাকা) ড্যাশবোর্ড দেখাবে 👇

```text
╔═══════════════════════════════════════════╗
║ VOTER EXTRACTOR          6 CORE 06:40 [|] ║
╠═══════════════════════════════════════════╣
║ PDF 175/683 (25%)  Unique 106,481         ║
║ Speed 0.4/s ETA 18:51 Failed 0            ║
╠═══════════════════════════════════════════╣
║ > 882084_com_1338_female_75_...       77% ║
║ > 882084_com_1380_male_78_...         75% ║
║ + 882085_com_353_male_20_...         100% ║
╠═══════════════════════════════════════════╣
║ Done: 882085_com_326_female_19... (+326)  ║
╚═══════════════════════════════════════════╝
```

- 📈 মোট অগ্রগতির শতাংশ
- 📄 কতটি PDF শেষ, মোট ইউনিক ভোটার, গতি, ETA ও Failed সংখ্যা
- ⚙️ চলমান প্রতিটি PDF-এর লাইভ ০→১০০%
- 📱 ফোনের স্ক্রিনের মাপ অনুযায়ী ড্যাশবোর্ড নিজে থেকে ছোট-বড় হয়, তাই লাইন ভেঙে এলোমেলো হয় না

> 💡 ভালো দেখতে Termux-এর ফন্ট সাইজ একটু ছোট রাখুন (স্ক্রিনে দুই আঙুল দিয়ে চিমটি কাটুন) বা ফোন আড়াআড়ি (landscape) করুন।

---

## 📤 ফলাফল কোথায় পাবেন?

`voters.zip` যে ফোল্ডারে আছে, ফলাফলও সেখানেই তৈরি হবে (`Votar` ফোল্ডার) 🎉

```text
📁 Votar/
├── 📦 voters.zip            (আপনার মূল ফাইল)
├── 🧾 voters.json           ✅ ভোটারদের সব রেকর্ড
├── 📝 suspect_report.txt    ⚠️ সন্দেহজনক / ভুল হতে পারে এমন লেখা
└── 🖼️ unknown_glyphs.png    🔎 অজানা অক্ষরের ছবি (থাকলে)
```

| ফাইল | কাজ |
|------|-----|
| 🧾 `voters.json` | PDF থেকে পাওয়া সব রেকর্ড |
| 📝 `suspect_report.txt` | সন্দেহজনক লেখার রিপোর্ট |
| 🖼️ `unknown_glyphs.png` | অজানা অক্ষরের ছবি (শুধু প্রয়োজন হলে তৈরি হয়) |

---

## 🔁 পরের বার চালাতে

সেটআপ একবারই করতে হয়। পরের বার শুধু Termux খুলে এটি দিন 👇

```bash
cd ~/pdf-ocr-tools- && python voter_extractor.py
```

---

## 🔄 কোড আপডেট করতে

```bash
cd ~/pdf-ocr-tools- && git pull
```

---

## 🛠️ সমস্যা সমাধান

<details>
<summary>📦 <b>voters.zip পাওয়া যাচ্ছে না</b></summary>

```bash
termux-setup-storage
ls -lh ~/storage/shared/Votar/
```

- ফাইলের নাম ঠিক `voters.zip` কি না দেখুন (`voters.zip.zip` বা `Voters.zip` হলে চলবে না)
- ফাইলটি `Votar` ফোল্ডারে আছে কি না দেখুন
- Permission চাইলে **Allow** দিন

</details>

<details>
<summary>🐍 <b>ModuleNotFoundError / pypdf নেই</b></summary>

```bash
cd ~/pdf-ocr-tools-
python -m pip install pypdf
```

</details>

<details>
<summary>📁 <b>git clone করার সময় "already exists" দেখাচ্ছে</b></summary>

আবার clone করবেন না। শুধু ফোল্ডারে ঢুকুন:

```bash
cd ~/pdf-ocr-tools-
```

</details>

<details>
<summary>❌ <b>অন্য কোনো Error</b></summary>

Termux-এর পুরো Error লেখাটি কপি করে সহায়তা নিন। চাইলে লগ ফাইলও দেখতে পারেন:

```bash
cat ~/pdf-ocr-tools-/voter_extractor.log
```

</details>

---

## 🔒 Privacy ও নিরাপত্তা

- 🚫 আসল `voters.zip` ও তৈরি `voters.json` **Public GitHub-এ আপলোড করবেন না**
- 📱 ব্যক্তিগত ভোটার ডাটা নিজের ফোনেই সংরক্ষণ করুন
- ⚖️ ডাটা ব্যবহারে প্রযোজ্য আইন ও অনুমতি মেনে চলুন

> `.gitignore` ফাইলে এগুলো আগে থেকেই বাদ দেওয়া আছে ✅

---

## 📁 প্রজেক্ট ফাইল

```text
pdf-ocr-tools-/
├── 🐍 voter_extractor.py   মূল স্ক্রিপ্ট
├── 📋 requirements.txt     লাইব্রেরি তালিকা
├── 📖 README.md            এই নির্দেশিকা
├── 📜 LICENSE
└── 🙈 .gitignore
```

---

## 👨‍💻 ডেভেলপার ও যোগাযোগ

<div align="center">

### 🧑‍💻 Forhad Khandokar

[![Telegram](https://img.shields.io/badge/Telegram-@forhadkhandakar-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/forhadkhandakar)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-+966_55_152_8982-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/966551528982)

| | যোগাযোগ |
|---|---|
| 👤 নাম | Forhad Khandokar |
| ✈️ Telegram | [@forhadkhandakar](https://t.me/forhadkhandakar) |
| 💬 WhatsApp | [+966 55 152 8982](https://wa.me/966551528982) |

📩 কোনো সমস্যা বা পরামর্শ থাকলে মেসেজ করুন!

</div>

---

<div align="center">

**🔗 GitHub:** https://github.com/jsfahad700-collab/pdf-ocr-tools-

⭐ কাজে লাগলে Repository-তে Star দিন!

</div>
