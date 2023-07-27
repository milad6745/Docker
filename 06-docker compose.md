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
