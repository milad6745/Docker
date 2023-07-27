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
