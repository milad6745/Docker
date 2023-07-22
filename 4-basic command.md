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


‍‍‍```
docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
3f3a23a43420   nginx     "/docker-entrypoint.…"   7 seconds ago    Exited (0) 3 seconds ago              thirsty_payne
```
##
