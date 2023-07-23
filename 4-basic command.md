## pull docker images and run container

```
docker run potgres
```

فرق بین کانتینر و ایمیج:
کانتینر تصویری از ایمیج است (کانتینر enviremant ایمیج است )
کانتینر توسط یک پورت به برنامه متصل میشود .
کانتینر یک فایل سیستم مجازی است.


## دانلود کردن یک ایمیج از داکر هاب

```
docker pull redis
```

## چک کردن ایمیج دانلود شده


```
docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
nginx         latest    021283c8eb95   2 weeks ago    187MB
python        latest    c0e63845ae98   5 weeks ago    1.01GB
hello-world   latest    9c7a54a9a43c   2 months ago   13.3kB
```

## اجرا کردن یک ایمیج
```
docker run nginx
```

## دیدن کانتینر های در حال اجرا


```

docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
3f3a23a43420   nginx     /docker-entrypoint.…   7 seconds ago    Exited (0) 3 seconds ago              thirsty_payne

```
##

## برای بردن کانتینر به مدل deatach برای اینکه کانتینر با کنترل سی استاپ نشود


```
docker run -d nginx
```
## استاپ و استارت کردن داکر


```
docker stop <container id>
docker start <container id>
```

## وقتی دو بار یک سرویس را اجرا میکنیم چه اتفاقی میافتد .
```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS      NAMES
55e85af7018c   redis     "docker-entrypoint.s…"   5 minutes ago    Up 5 minutes    6379/tcp   zealous_colden
b88616c8b4a7   redis     "docker-entrypoint.s…"   5 minutes ago    Up 5 minutes    6379/tcp   zealous_cori
64cf463c5ba0   redis     "docker-entrypoint.s…"   22 minutes ago   Up 19 minutes   6379/tcp   elastic_saha
```
در اینجا ما سه بار کانتینر ردیس را ران کردیم و پ.رت 6379 سه بار باز شده است . حال چگونه کانفلیکت ایجاد نمیشود.
برای این کار باید از پورت مپینگ استفاده شود . اینگونه که مثلا ما پورت 6000 را به یک کانتینر و پورت 5000 را از سرور هاست خود به کانتینر متصل میکنیم .

```
docker run -p6000:6379
docker run -p5000:6379

docker ps -a
0c54dd1d2d05   redis     "docker-entrypoint.s…"   11 seconds ago   Up 10 seconds               0.0.0.0:5000->6379/tcp   charming_leavitt
b2899d44680f   redis     "docker-entrypoint.s…"   27 seconds ago   Up 26 seconds               0.0.0.0:6000->6379/tcp   elegant_sino
```

