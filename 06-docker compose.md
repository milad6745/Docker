اجرا مثال قبل به وسیله داکر کامپوز : داکر کامپوز برای اجرای تعداد زیادی کانتینر که قرار است با هم ارتباط داشته باشند بکار میرود .
```

version: '3.8'          #docker compose version
services:
  mongodb:              #docker container name
    image: mongo:latest # use the latest image.
    container_name: mongodb
    environment: # set required env variables to access mongo
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: password
    ports:

   - 27017:27017
     mongo-express:
         image: mongo-express:latest # latest image
         restart: unless-stopped
         ports:
        - 8081:8081
          vironment:
                ME_CONFIG_MONGODB_ADMINUSERNAME: root
                ME_CONFIG_MONGODB_ADMINPASSWORD: password
                ME_CONFIG_MONGODB_SERVER: mongodb
```
برای اجرای داکر کامپوز از دستور زیر استفاده میکنیم
```
docker-compose up -d
```
برای اینکه کارهایی که داکر کامپوز انجام داده را از بین ببریم و استاپ کنیم 
```
docker-compose down
```



برای توضیح بیشتر، یک مثال از فایل `docker-compose.yaml` را ارائه می‌دهم. در این مثال، یک برنامه ساده تشکیل شده از دو سرویس (یک وب‌سرور و یک پایگاه داده) را با استفاده از Docker Compose تعریف می‌کنیم.

1. ابتدا، یک پوشه برای پروژه خود ایجاد کنید و وارد آن شوید.

```bash
mkdir my-compose-project
cd my-compose-project
```

2. یک فایل به نام `docker-compose.yaml` ایجاد کنید و با ویرایشگر متن مورد علاقه خود باز کنید.

```bash
nano docker-compose.yaml
```

3. سپس کد زیر را درون فایل `docker-compose.yaml` قرار دهید:

```yaml
version: "3.8"

services:
  web-server:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./web-content:/usr/share/nginx/html

  database:
    image: postgres:latest
    environment:
      POSTGRES_DB: mydatabase
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
    name: mydatabase-data
```

در این مثال:

- `web-server`: یک سرویس وب‌سرور Nginx که به پورت 8080 از میزبان متصل می‌شود و محتوای وب را از پوشه `./web-content` در میزبان مانیتور می‌کند.

- `database`: یک سرویس پایگاه داده PostgreSQL که یک دیتابیس به نام `mydatabase` را ایجاد می‌کند و اطلاعات دائمی را در یک حجم به نام `db-data` ذخیره می‌کند.

4. ذخیره و خروج از ویرایشگر و سپس با دستور زیر Docker Compose را اجرا کنید:

```bash
docker-compose up
```

این دستور، تمام سرویس‌ها را بر اساس تعریفات در فایل `docker-compose.yaml` اجرا خواهد کرد. شما می‌توانید وب‌سرور را با مراجعه به `http://localhost:8080` و یا به هر آدرسی که در مرورگر خود تنظیم کرده‌اید، دسترسی پیدا کنید.

5. برای خاتمه کار و توقف تمام سرویس‌ها، از دستور زیر استفاده کنید:

```bash
docker-compose down
```

این مثال نشان دهنده نحوه استفاده از Docker Compose برای تعریف و مدیریت یک پروژه چندسرویسه در Docker است.
