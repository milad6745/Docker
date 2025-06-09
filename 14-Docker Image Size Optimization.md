کاهش حجم یک **ایمیج داکر (Docker Image)** یکی از مهم‌ترین مراحل بهینه‌سازی در توسعه و دیپلوی اپلیکیشن‌ها است. در ادامه **تمام راهکارهای موثر و عملی** برای کاهش حجم ایمیج‌های Docker را به‌صورت طبقه‌بندی‌شده ارائه می‌دهم:

---

## 🧱 1. انتخاب پایه (Base Image) مناسب

بزرگ‌ترین عامل در حجم اولیه ایمیج، **Base Image** است.

### راهکارها:

* استفاده از **`alpine`** به‌جای ایمیج‌های معمول (مثل `ubuntu` یا `debian`):

  ```Dockerfile
  FROM node:alpine
  ```
* بررسی نیازهای اپلیکیشن؛ اگر به ابزارهای زیاد نیاز ندارید، `alpine` بهترین گزینه است (حدود 5MB).
* از ایمیج‌های **slim** استفاده کنید (مثل `python:3.11-slim`).

---

## 📦 2. چند مرحله‌ای (Multi-stage Build)

با استفاده از **multi-stage builds** می‌توانید بخش Build و Runtime را از هم جدا کنید.

### مثال:

```Dockerfile
# مرحله اول - کامپایل و ساخت
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# مرحله دوم - فقط باینری نهایی
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

🔽 این کار باعث می‌شود فایل‌های build، compiler، و dependencyهای غیرضروری وارد ایمیج نهایی نشوند.

---

## 🔥 3. حذف فایل‌ها و کش‌های موقتی

بعد از نصب یا build، فایل‌های موقتی را حذف کنید.

### مثال:

```Dockerfile
RUN apt-get update && apt-get install -y some-package \
 && rm -rf /var/lib/apt/lists/*
```

---

## 🧹 4. فشرده‌سازی لایه‌ها

هر دستور در Dockerfile یک لایه ایجاد می‌کند. استفاده‌ی زیاد از `RUN`, `COPY`, `ADD` باعث افزایش حجم می‌شود.

### راهکار:

* **دستورهای ترکیبی بنویسید**:

  ```Dockerfile
  RUN apt-get update && apt-get install -y curl git && rm -rf /var/lib/apt/lists/*
  ```

---

## 🧱 5. فقط فایل‌های موردنیاز را کپی کنید

از `.dockerignore` برای جلوگیری از کپی شدن فایل‌های غیرضروری استفاده کنید.

### مثال:

`.dockerignore`:

```
.git
node_modules
*.log
.env
```

---

## 🪛 6. استفاده از باینری‌های استاتیک و Minify شده

برای زبان‌هایی مثل Go، Rust، C++:

* باینری را با `strip` کوچک کنید.
* باینری statically compiled بسازید تا به داینامیک لینک نیاز نداشته باشد.

---

## 📁 7. حذف dependencyهای dev

مثلاً در Node.js:

```Dockerfile
RUN npm install --production
```

یا برای Python:

```Dockerfile
RUN pip install -r requirements.txt --no-cache-dir
```

---

## 🔍 8. بررسی سایز لایه‌ها با ابزارها

### ابزارهای پیشنهادی:

* [`dive`](https://github.com/wagoodman/dive): بررسی لایه به لایه ایمیج
* `docker image history <image>`: تاریخچه لایه‌ها

---

## 🧬 9. استفاده از ابزارهای Build پیشرفته

### مثل:

* **BuildKit**:

  ```bash
  DOCKER_BUILDKIT=1 docker build .
  ```

  سریع‌تر، بهینه‌تر و با کش بهتر.

* **docker-slim**: فشرده‌سازی خودکار ایمیج‌ها

  ```bash
  docker-slim build your-image
  ```

---

## 🗃️ 10. فایل‌های تنظیمات و اسکریپت‌های نصب را تمیز کنید

مثلاً اگر از bash scripts یا فایل config موقتی استفاده می‌کنید، در پایان حذفشان کنید.

---

## 🔧 11. به‌روزرسانی ایمیج و پاک‌سازی بسته‌ها

از آپدیت بی‌مورد base image اجتناب کنید مگر اینکه لازم باشد؛ اگر لازم است:

```Dockerfile
RUN apt-get update && apt-get upgrade -y && apt-get clean && rm -rf /var/lib/apt/lists/*
```

---

## ✅ جمع‌بندی

| روش                             | تأثیر | توضیح                         |
| ------------------------------- | ----- | ----------------------------- |
| استفاده از `alpine`             | ⭐⭐⭐⭐  | ایمیج بسیار سبک               |
| Multi-stage Build               | ⭐⭐⭐⭐⭐ | ساخت حرفه‌ای و تمیز           |
| استفاده از `.dockerignore`      | ⭐⭐⭐   | جلوگیری از کپی فایل‌های اضافی |
| فشرده‌سازی لایه‌ها              | ⭐⭐    | کاهش لایه‌های حجیم            |
| استفاده از ابزار `dive`, `slim` | ⭐⭐⭐⭐  | تحلیل و کاهش سایز دقیق        |
| حذف کش و فایل‌های موقتی         | ⭐⭐⭐   | حذف فایل‌های غیرضروری         |

---

اگر مایل باشید، می‌توانم یک نسخه سبک شده از Dockerfile فعلی‌تان را نیز بازنویسی کنم. فقط کافیست آن را بفرستید.
