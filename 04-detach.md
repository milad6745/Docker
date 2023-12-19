# چگونگی استفاده از حالت Detached

یک گزینه بسیار محبوب دیگر از دستور run، گزینه --detach یا -d است. در مثال بالا، برای اینکه کانتینر ادامه به کار داشته باشد، شما باید پنجره ترمینال را باز نگه داشته باشید. بستن پنجره ترمینال همچنین منجر به توقف کانتینر در حال اجرا می‌شد.

این به دلیل این است که به صورت پیش‌فرض، کانتینرها در پس‌زمینه اجرا شده و خود را به ترمینال متصل می‌کنند، مانند هر برنامه عادی دیگری که از ترمینال فراخوانی شود.

برای تغییر این رفتار و اجرای یک کانتینر در پس‌زمینه، می‌توانید گزینه --detach را با دستور run به صورت زیر استفاده کنید:

```
docker container run --detach --publish 8080:80 fhsinchy/hello-dock
# 9f21cb77705810797c4b847dbd330d9c732ffddba14fb435470567a7a3f46cdc
```