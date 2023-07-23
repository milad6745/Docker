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
