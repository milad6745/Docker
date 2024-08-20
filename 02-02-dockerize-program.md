#  Dockerize a Program
قدم 1: ایجاد کد اپلیکیشن
برای این مثال، ما یک اپلیکیشن ساده در زبان پایتون می‌نویسیم که یک وب سرور اجرا می‌کند و درخواست‌های HTTP را پاسخ می‌دهد. این اپلیکیشن به درخواست‌ها پاسخ "Hello, Docker!" می‌دهد.

1.1. ایجاد پرونده `app.py` با محتوای زیر:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello, Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

قدم 2: نصب و تنظیم Docker
اگر Docker را نصب ندارید، ابتدا آن را بر روی سیستم خود نصب کنید. برای نصب Docker روی سیستم‌های Ubuntu، می‌توانید از دستورات زیر استفاده کنید:

2.1. نصب Docker:

```bash
sudo apt update
sudo apt install docker.io
```

2.2. راه‌اندازی Docker سرویس:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

قدم 3: ایجاد فایل تنظیمی Docker
حالا نیاز داریم یک فایل تنظیمی Docker برای ساخت و اجرای کانتینر اپلیکیشن ایجاد کنیم.

3.1. ایجاد پرونده `Dockerfile` با محتوای زیر:

```Dockerfile
# انتخاب تصویر پایه (base image) برای اجرای اپلیکیشن
FROM python:3.8-slim

# کپی کد اپلیکیشن به داخل کانتینر
COPY app.py /app.py

# نصب وابستگی‌های اپلیکیشن
RUN pip install Flask

# تنظیمات محیطی
ENV FLASK_APP=/app.py

# پورتی که اپلیکیشن باید در آن اجرا شود
EXPOSE 5000

# دستور اجرای اپلیکیشن
CMD ["flask", "run", "--host", "0.0.0.0"]
```

قدم 4: ساخت تصویر Docker
در این مرحله، ما یک تصویر Docker از اپلیکیشن خود ایجاد خواهیم کرد.

4.1. باز کنسول ترمینال و در دایرکتوری محتویات پرونده‌های `app.py` و `Dockerfile` باشید.

4.2. برای ساخت تصویر، دستور زیر را اجرا کنید:

```bash
docker build -t my-docker-app .
```

قدم 5: اجرای کانتینر
حالا که تصویر Docker ساخته شده است، می‌توانیم آن را به صورت یک کانتینر اجرا کنیم.

5.1. اجرای کانتینر:

```bash
docker run -d -p 5000:5000 my-docker-app
```
OR
```yml
version: '3.8'

services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "500:5000"
```

حالا اپلیکیشن شما در داخل یک کانتینر Docker در حال اجراست و می‌توانید از طریق مرورگر وارد آدرس http://localhost:5000 شوید تا پیام "Hello, Docker!" را مشاهده کنید.
