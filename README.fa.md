# Paqet-Tunnel-Manager

اسکریپت مدیریتی برای **paqet**: یک تونل مبتنی بر Raw Socket و KCP که برای عبور از فایروال و DPI طراحی شده است. این اسکریپت از سناریوی **سرور خارج (Kharej)** و **کلاینت ایران (Entry Point)** پشتیبانی می‌کند.

توضیحات آپدیت ها فقط در تلگرام داده میشود.
کانال تلگرام:
https://t.me/BehzadEa12
---

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.3.0-blue?style=for-the-badge&logo=linux" alt="Version">
  <img src="https://img.shields.io/badge/Platform-Linux-orange?style=for-the-badge" alt="Platform">
  <img src="https://img.shields.io/github/stars/behzadea12/Paqet-Tunnel-Manager?style=for-the-badge&color=yellow" alt="Stars">
  <img src="https://img.shields.io/github/forks/behzadea12/Paqet-Tunnel-Manager?style=for-the-badge&color=green" alt="Forks">
</p>

## فهرست مطالب

* [شروع سریع](#شروع-سریع)
* [مراحل نصب](#مراحل-نصب)

  * [مرحله ۱: راه‌اندازی سرور خارج (Kharej – VPN Server)](#مرحله-۱-راهاندازی-سرور-خارج-kharej--vpn-server)
  * [مرحله ۲: راه‌اندازی سرور ایران (Iran – Client/Entry Point)](#مرحله-۲-راهاندازی-سرور-ایران-iran--cliententry-point)
* [تنظیمات پیشرفته (حالت‌های KCP)](#تنظیمات-پیشرفته-حالتهای-kcp)
* [بهینه‌سازی شبکه (اختیاری)](#بهینهسازی-شبکه-اختیاری)
* [ابزارهای استفاده‌شده](#ابزارهای-استفادهشده)
* [عیب‌یابی: مشکلات نصب Paqet](#عیبیابی-مشکلات-نصب-paqet)
* [نیاز به کمک؟](#️-نیاز-به-کمک)
* [پیش‌نیازها](#پیشنیازها)
* [تصائیر اسکریپت](#-تصاویر-اسکریپت)
* [لایسنس](#لایسنس)
* [قدردانی](#قدردانی)
---

## شروع سریع

اسکریپت را روی **هر دو سرور** و با دسترسی **root** اجرا کنید:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)
```


> ورژن قدیمی  (3.8) - اگر با ورژن جدید مشکلی دارید میتونید از این استفاده کنید: 
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager3-8.sh)
```

سپس **گزینه 0** و بعد **گزینه 1** را برای نصب پیش‌نیازها انتخاب کنید.

---

## مراحل نصب

### مرحله ۱: راه‌اندازی سرور خارج (Kharej – VPN Server)

اسکریپت را اجرا کنید:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)
```

#### مراحل پیکربندی

1. **گزینه 2** را انتخاب کنید (Kharej)
2. **یک نام دلخواه** برای سرویس/تونل وارد کنید (مثال: `fanland1`)
3. **پورت Listen** را وارد کنید (مثال: `443` یا `8443`)
4. برای ساخت خودکار **Secret Key**، **Enter** بزنید
5. **کلید ساخته‌شده را ذخیره کنید** سپس **`Y`** را برای تأیید بزنید
6. **حالت KCP** را انتخاب کنید (پیشنهادی: گزینه `1` - fast)
7. **conn value** → تعداد اتصال‌های KCP (مثال: `4`)
8. **MTU** → مقدار پیش‌فرض `1350` (در صورت نیاز می‌توانید مثلاً `1200` وارد کنید)
9. **متد Encryption** را انتخاب کنید (پیش‌فرض: `aes-128-gcm`)
10. **pcap sockbuf** → برای مقدار پیش‌فرض **Enter** بزنید
11. **transport tcpbuf** → برای مقدار پیش‌فرض **Enter** بزنید
12. **transport udpbuf** → برای مقدار پیش‌فرض **Enter** بزنید

---

### مرحله ۲: راه‌اندازی سرور ایران (Iran – Client/Entry Point)

اسکریپت را اجرا کنید:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)
```
#### مراحل پیکربندی

1. **گزینه 3** را انتخاب کنید (Iran)
2. **یک نام دلخواه** برای سرویس/تونل وارد کنید (مثال: `fanland`)
3. **آی‌پی سرور خارج** را وارد کنید (مثال: `65.109.206.29`)
4. **پورت سرور** (پورت ارتباطی بین دو سرور) را وارد کنید (مثال: `443`)
5. **کلید سکرت** که روی سرور خارج ساخته شده را وارد کنید
6. **حالت KCP** را انتخاب کنید (پیشنهادی: گزینه `1` - fast)
7. **conn value** → تعداد اتصال‌های KCP (پیش‌فرض: `1`)
8. **MTU** → مقدار پیش‌فرض `1350` (Enter بزن)
9. **متد Encryption** را انتخاب کنید (پیش‌فرض: `aes-128-gcm`)
10. **pcap sockbuf** → برای مقدار پیش‌فرض **Enter** بزنید
11. **transport tcpbuf** → برای مقدار پیش‌فرض **Enter** بزنید
12. **transport udpbuf** → برای مقدار پیش‌فرض **Enter** بزنید
13. **پورت یا پورت‌های Forward** را وارد کنید
    تک پورت: `333` — چند پورت: `333,394,395`
14. **برای هر پورت، پروتکل را انتخاب کنید**
    `1` tcp — `2` udp — `3` tcp/udp

---


آپدیت (میتونید بعد تانل اینکار رو انجام بدید - میتونید قبلش انجام بدید تفاوتی وجود نداره - اگر قبل تانل زدید دیگه نیاز به نصب هسته مجدد ندارید!):

نصب هسته کاستومایز شده و بهینه شده:

جهت نصب از طریق URL:

لینک معماری سرورتون رو کپی کنید:

linux-amd64:
```bash
https://github.com/behzadea12/Paqet-Tunnel-Manager/releases/download/PaqetOptimized/paqet-linux-amd64-v2.2.0-optimize.tar.gz
```
linux_arm64:
```bash
https://github.com/behzadea12/Paqet-Tunnel-Manager/releases/download/PaqetOptimized/paqet_linux_arm64-v2.2.0-optimize.tar.gz
```
1- وارد اسکریپت بشید
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)

```
2- گزینه 0 رو وارد کنید (Install Paqet Binary / Manager)

3- گزینه 3 رو وارد کنید (Download from custom URL)

4- لینک رو پیست کنید و اینتر بزنید و منتظر بمونید تا دانلود بشه بستگی به سرورتون داره مدت زمانش.

5-برید به منوی اصلی اسکریپت - سرویستون رو ریستارت کنید. - اگر تعداد زیادی سرویس دارید از بخش 5 میتونید گزینه 10 رو بزنید که همشون به صورت خودکار ریستارت بشن
.
من معذرت میخوام از همه دوستانی که این متن رو میخونید چون درست نیست. - هرکس که این نسخه از هسته و یا اسکریپت من رو برای فروش بگذارد بیانگر مادر اشتراکی خود هست - سو استفاده نکنید - انسان باشید.

نکته: هسته هم در سرور خارج هم در ایران باید یکی باشه.

---


## تنظیمات پیشرفته (حالت‌های KCP)

در **مرحله 8 (سرور خارج)** و **مرحله 9 (سرور ایران)** می‌توانید حالت‌های مختلف KCP را انتخاب کنید.

### حالت‌های KCP

0. **normal** – سرعت نرمال، تأخیر نرمال، مصرف منابع کم
1. **fast** – سرعت متعادل، تأخیر کم، مصرف منابع نرمال
2. **fast2** – سرعت بالا، تأخیر کمتر، مصرف منابع متوسط
3. **fast3** – حداکثر سرعت، تأخیر بسیار کم، مصرف CPU بالا
4. **manual** – تنظیمات پیشرفته به‌صورت دستی

> **پیشنهاد:**
> طبق بازخورد کاربرانی که از این اسکریپت استفاده کرده‌اند، **گزینه 1 (fast)** در اکثر شرایط بهترین عملکرد را دارد.
> اگر **سرور ایران شما محدودیت شبکه یا منابع** دارد، پیشنهاد می‌شود حالت‌های مختلف را تست کنید.
> در صورتی که **دانش فنی و تجربه کافی** دارید، می‌توانید از **manual** برای تنظیم دقیق همه پارامترها استفاده کنید.



---

## بهینه‌سازی شبکه (اختیاری)

اسکریپت را اجرا کنید:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)
```

سپس **گزینه 7** را انتخاب کرده و یکی از موارد زیر را انتخاب کنید:

1. **BBR** – بهینه‌ساز کنترل ازدحام TCP *(پیشنهادی برای سرور خارج)*
2. **DNS Finder** – یافتن بهترین DNS برای ایران *(پیشنهادی برای سرور ایران)*
3. **Mirror Selector** – یافتن سریع‌ترین مخزن APT *(پیشنهادی برای سرور ایران)*

---

## ابزارهای استفاده‌شده

* **BBR – TCP Congestion Control Optimizer**
  [https://github.com/teddysun/across/](https://github.com/teddysun/across/)

* **IranDNSFinder – یافتن و تنظیم بهترین DNSها برای ایران**
  [https://github.com/alinezamifar/IranDNSFinder](https://github.com/alinezamifar/IranDNSFinder)

* **DetectUbuntuMirror – انتخاب سریع‌ترین APT Mirror (Ubuntu/Debian)**
  [https://github.com/alinezamifar/DetectUbuntuMirror](https://github.com/alinezamifar/DetectUbuntuMirror)

---
## عیب‌یابی: مشکلات نصب Paqet

اگر در هنگام پیکربندی، نصب Paqet به‌صورت خودکار انجام نشد
(مثلاً پیام **"Failed to install Paqet"** نمایش داده شد یا اسکریپت هنگام افزودن کانفیگ در حالت **Kharej** یا **Iran** متوقف شد)، مراحل زیر را انجام دهید:

---

### 1. دانلود دستی فایل Paqet

به صفحه ریلیز رسمی مراجعه کنید:
[https://github.com/hanselime/paqet/releases](https://github.com/hanselime/paqet/releases)

* **آخرین نسخه** را دانلود کنید.
* فایل متناسب با معماری سرور خود را انتخاب کنید:

  * `paqet-linux-amd64-*.tar.gz` → برای سرورهای 64 بیتی (x86_64 / amd64)
  * `paqet-linux-arm64-*.tar.gz` → برای سرورهای ARM (aarch64 / arm64)

### 2. قرار دادن فایل در مسیر مشخص‌شده

فایل دانلودشده را در مسیر زیر قرار دهید:

```bash
/root/paqet/
```

اگر این پوشه وجود ندارد، ابتدا آن را بسازید:

```bash
mkdir -p /root/paqet
```

### 3. اجرای مجدد اسکریپت

اسکریپت به‌صورت خودکار فایل موجود در `/root/paqet/` را شناسایی کرده، استخراج می‌کند و نصب را کامل می‌کند:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/behzadea12/Paqet-Tunnel-Manager/main/paqet-manager.sh)
```

---

### 4. خطای GLIBC_2.32 یا GLIBC_2.34 not found

اگر سرویس با خطایی مشابه زیر متوقف شد:

```
/usr/local/bin/paqet: version `GLIBC_2.34' not found
```

یعنی نسخه glibc سیستم شما قدیمی‌تر از نسخه موردنیاز باینری Paqet است
(مثلاً Ubuntu 18.04 یا Debian 10).

#### راه‌حل اول: ارتقای سیستم‌عامل

سیستم‌عامل را به توزیعی با glibc 2.34+ ارتقا دهید:

* Ubuntu 22.04 یا جدیدتر
* Debian 12 یا جدیدتر

سپس دوباره Paqet را با منیجر (گزینه 0) نصب کنید.

#### راه‌حل دوم: کامپایل از سورس روی همان سرور

برای اینکه Paqet با glibc فعلی سیستم شما لینک شود:

```bash
apt install -y golang git
git clone https://github.com/hanselime/paqet.git && cd paqet
go build -o paqet ./cmd/paqet
sudo cp paqet /usr/local/bin/paqet
sudo chmod +x /usr/local/bin/paqet
```

سپس سرویس Paqet را دوباره استارت کنید:

List Services → Manage → Start

#### راه‌حل سوم: استفاده از VPS جدیدتر

از یک VPS با توزیع جدیدتر (مثلاً Ubuntu 22.04) استفاده کرده و Paqet را روی آن نصب کنید.

---

### 5. خطای bind: address already in use (پورت در حال استفاده است)

اگر Paqet با خطایی مشابه زیر متوقف شد:

```
failed to bind TCP socket on 0.0.0.0:8443: bind: address already in use
```

یعنی آن پورت (مثلاً 8443) روی همان سرور قبلاً توسط برنامهٔ دیگری استفاده می‌شود، یا همان پورت دو بار در لیست forward وارد شده است.

#### بررسی استفاده از پورت

```bash
ss -tuln | grep 8443
```

یا

```bash
lsof -i :8443
```

اگر سرویس دیگری (مثلاً nginx، وب‌سرور، یا V2Ray) روی آن پورت فعال است، یا آن سرویس را متوقف کنید یا در کانفیگ Paqet پورت دیگری انتخاب کنید.

#### حذف پورت تکراری

اگر پورتی دو بار در لیست پورت‌ها وارد شده است:

* فایل کانفیگ را ویرایش کنید:

```bash
nano /etc/paqet/نام_کانفیگ.yaml
```

* در بخش `forward:`، هر خطی که همان پورت را دوباره `listen` می‌کند حذف کنید.
* سپس سرویس را ریستارت کنید:

```bash
systemctl restart paqet-نام_کانفیگ
```

در نسخه‌های جدید اسکریپت، پورت‌های تکراری به‌صورت خودکار حذف می‌شوند.

---

## ⚠️ نیاز به کمک؟

در صورت بروز هرگونه مشکل، از طریق تلگرام با من در ارتباط باشید:

**@behzad_developer**

معمولاً آنلاین هستم و در سریع‌ترین زمان ممکن کمکتان می‌کنم.

---

## پیش‌نیازها

* سرور لینوکسی (Ubuntu، Debian، CentOS و ...)
* دسترسی root
* `libpcap-dev`
* `iptables`
* `paqet`

---

## 📸 تصاویر اسکریپت

<details>
<summary>منو اصلی</summary>
<br>
<img src="images/Main_Menu.png" width="800">
</details>

<details>
<summary>منوی نصب Paqet</summary>
<br>
<img src="images/Install_paqet.png" width="800">
</details>

<details>
<summary>منو سرویس ها</summary>
<br>
<img src="images/List_Services.png" width="800">
</details>

<details>
<summary>منو مدیریت سرویس ها</summary>
<br>
<img src="images/Manage_Service.png" width="800">
</details>

<details>
<summary>منو بهینه سازی سرور</summary>
<br>
<img src="images/Optimize_Server.png" width="800">
</details>

---

## لایسنس

این پروژه تحت **لایسنس MIT** منتشر شده است.

---

## 💖 حمایت مالی / Support / Donate

اگر از **Paqet-Tunnel-Manager** استفاده می‌کنید و می‌خواهید از توسعه این پروژه حمایت کنید، می‌توانید از طریق موارد زیر کمک کنید:

<details>
<summary>💰 ارز دیجیتال / Crypto</summary>
<br>

* **Tron (TRC20):**
  `TFYnorJt5gvejLwR8XQdjep1krS9Zw8pz3`

</details>

---
> هر حمایتی، کوچک یا بزرگ، به ادامه پروژه کمک می‌کند و انگیزه تیم توسعه را افزایش می‌دهد. 🙏

## قدردانی

* **paqet** – کتابخانه تونل‌سازی Raw Packet نوشته‌شده توسط hanselime
  [https://github.com/hanselime/paqet](https://github.com/hanselime/paqet)
