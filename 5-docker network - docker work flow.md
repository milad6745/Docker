 ## توضیح
مامیخواهیم به وسیله یک کانتینر nodjs و اپلیکیشتنی که نوشتیم را به یک دیتا بیس مونگو که داکری است متصل کنیم . برای این کار ابتدا دو ایمیج mongo , mongo-express  را دانلود و ران میکنیم

![image](https://github.com/milad-baousi/Docker/assets/113288076/7e0ddfa1-5efe-44a4-87cb-14206743ee3b)

```
docker pull mongo
docker pull mongo-express
```

برای این کار باید مونگو و مونگو اکسپرس و nodejs ما داخل یک شبکه باشد . که میبایست اینگونه عمل کنیم .

```
docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
bbb799d57d6a   bridge    bridge    local
725fbe0ae5e3   host      host      local
74c4c321a5bc   none      null      local
```

حال ما باید نتورک خودمان را برای این ارتباط ایجاد کنیم.
```
docker network create mongo-network
docker network ls
NETWORK ID     NAME            DRIVER    SCOPE
671c5c9ccc7f   mongo-network   bridge    local
```

حال کانتیتر مونگو را ایجاد میکنیم.

‍‍‍```
docker run -d 
-p 27020:27020 
-e MONGO_INITDB_ROOT_USERNAME=admin 
-e MONGO_INITDB_ROOT_PASSWORD=password 
--network mongo-network 
--name mongodb 
mongo
‍‍‍‍‍‍```
سپس برای بررسی لاگ کانتینر را میخانیم.

```
docker logs mongodb
{"t":{"$date":"2023-07-23T14:16:42.075+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
```
حال کانتینر مونگو اکسپرس را ایجاد میکنیم.

```
docker run -d  \
    --network mongo-network \
    --name mongo-express \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \        
    -e ME_CONFIG_BASICAUTH_USERNAME=admin \
    -e ME_CONFIG_BASICAUTH_PASSWORD=password \
    mongo-express
```

سپس برای بررسی اتصال لاگ را مشاهده میکنیم.

## docker-compose
اجرا مراحل بالا به وسیله داکر کامپوز : داکر کامپوز برای اجرای تعداد زیادی کانتینر که قرار است با هم ارتباط داشته باشند بکار میرود .

‍‍‍```
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
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: password
      ME_CONFIG_MONGODB_SERVER: mongodb 
```

اجرا کردن داکر کامپوز :

‍‍‍```
docker-compose up -f
docker-compose -f filename up
```

خال متوجه میشویم که ما وقتی نام شبکه را قرار ندادیم یک شبکه به نام my app default ایجاد کرده است .

```
docker network ls
Creating network "root_default" with the default driver
Creating root_mongo-express_1 ... done
Creating root_mongodb_1       ... done
```


و در نهایت مونگو اکسپری ایجاد میشود.


![Screenshot from 2023-07-23 23-00-38](https://github.com/milad-baousi/Docker/assets/113288076/56355638-d2fa-419a-b04f-6dafd692f5dc)

