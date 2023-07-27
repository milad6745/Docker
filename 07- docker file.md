## docker file
برای بسته بندی یک پکیج در یک image استفاده میشود و سپس آن را به یک docker repository هل میدهیم .

برای ساخت یک داکر فایل باید محتویات برنامه را داخل داکر فایل کپی کنیم ، و آن را کانفیگ میکنیم .

FROM node:13-alpine #image name
ENV MONGO_INITDB_ROOT_USERNAME: root \
    MONGO_INITDB_ROOT_PASSWORD: password #better env on docker-compose

RUN mkdir -p /home/app # create a directory on container
COPY . /home/app # copy current files to this path
CMD ["node","server.js"] #start app with node

تفاوت CMD با RUN در این است که CMD یک entry point command آست .
میتوانیم تعداد زیادی RUN داشته باشیم اما CMD فقط یک خط فرمان است .

حال برای ساخت ایمیجمان با استفاده از داکر فایل
```
docker build -t myapp:1.0 dockerfile
```
