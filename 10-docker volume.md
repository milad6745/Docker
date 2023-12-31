# docker volume
با استفاده از داکر والیوم سایز ایمیج هایمان افزایش پیدا نمیکند و آنها را در هاست نگه داری میکنیم
![types-of-mounts-volume](https://github.com/milad-baousi/Docker/assets/113288076/a7bc1a50-cef2-4059-ae2b-bab5d0779427)

**چه زمانی از داکر والیوم استفاده میکنیم**
وقتی میخواهیم کانتینر را پاک کنیم یا ریستارت کنیم دیتای داخل آن از بین میرود و به حالت اول برمیگردد و اینجاست که به داکر والیوم نیاز پیدا میکنیم .
وقتی کانتینر با فایل های والیوم شده کار دارد آنها را از هاست خود دریافت میکند .

**Docker volume Types**

1- host volume :
docker run -v /home/mount/data:/var/lib/mysql/data
شما تصمیم میگیرید از کدام دایرکتوری به کجا والیوم شود.

2- anonymous volume


3-named volume


**docker compose volume**
```
services:
  frontend:
    image: node:lts
    volumes:
      - myapp:/home/node/app
volumes:
  myapp:
    external: true
```
```
 docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```



در Docker، ولوم‌ها (Volumes) به شما این امکان را می‌دهند که داده‌های داخل یک کانتینر را در یک مکان جداگانه و پایدار نگه دارید. ولوم‌ها از آنجایی که خودشان به عنوان یک موجودیت مستقل در Docker مدیریت می‌شوند، امکانات زیادی را برای مدیریت داده‌ها و اشتراک آنها بین کانتینرها فراهم می‌کنند.

### ایجاد ولوم:

برای ایجاد یک ولوم در Docker از دستور `docker volume create` استفاده می‌شود. به عنوان مثال:

```bash
docker volume create my_volume
```

در اینجا `my_volume` نام ولوم است. شما همچنین می‌توانید گزینه‌های دیگری را نیز اعمال کنید تا محدودیت‌های مختلف (مانند اندازه، راستریکت بر روی مسیر فیزیکی، و ...) را تنظیم کنید.

### لیست کردن ولوم‌ها:

برای مشاهده لیست ولوم‌های موجود، از دستور `docker volume ls` استفاده کنید:

```bash
docker volume ls
```

### نحوه اتصال یک ولوم به یک کانتینر:

می‌توانید یک ولوم را به یک کانتینر متصل کنید در زمان اجرا با استفاده از گزینه `-v` یا `--volume`. به عنوان مثال:

```bash
docker run -v my_volume:/path/in/container my_image
```

در اینجا `my_volume` نام ولوم است و `/path/in/container` مسیری است که داده‌های ولوم درون کانتینر قرار می‌گیرند.

### حذف ولوم:

برای حذف یک ولوم از دستور `docker volume rm` استفاده می‌کنیم. به عنوان مثال:

```bash
docker volume rm my_volume
```

### نکات مهم:

- **انواع ولوم**: Docker انواع مختلفی از ولوم‌ها را پشتیبانی می‌کند، از جمله ولوم‌های محلی (local volumes)، ولوم‌های متصل به شبکه (network volumes)، و ولوم‌های مربوط به درایوها (driver volumes).
  
- **اشتراک ولوم بین کانتینرها**: اگر چندین کانتینر به یک ولوم متصل شوند، تغییرات در یک کانتینر به صورت خودکار در دیگر کانتینرها هم قابل مشاهده خواهد بود.

- **استفاده از ولوم‌ها برای داده‌های پایدار**: از ولوم‌ها می‌توانید برای ذخیره داده‌های پایدار استفاده کنید، به جای استفاده از دایرکتوری‌های هنرامی.

- **حذف کانتینر ولوم**: اگر یک کانتینر با یک ولوم متصل شده باشد و کانتینر حذف شود، ولوم خودکار حذف نخواهد شد. باید به صورت جداگانه ولوم را حذف کنید.

این توضیحات مختصری از Docker Volumes است، و امکانات بیشتری وجود دارد که می‌توانید برای نیازهای خاص خود مطالعه کنید.
