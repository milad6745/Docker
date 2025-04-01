
---

### 📌 **Load Balancing و Ingress Networking در داکر**

Load Balancing به این معنیه که وقتی چند کانتینر مشابه داری (مثلاً چند سرور Nginx برای مدیریت ترافیک)، ترافیک به‌صورت خودکار بین اون‌ها توزیع بشه.

#### 📌 **دو روش اصلی برای Load Balancing توی داکر:**
1. **Load Balancing محلی (Local Load Balancing)**
2. **Ingress Load Balancing (ویژه Docker Swarm)**

---

## 1. **Load Balancing محلی (Local Load Balancing)**

وقتی از یک شبکه Bridge یا Custom Bridge استفاده می‌کنی، Load Balancing به صورت خودکار پشتیبانی نمی‌شه، اما اگه از یه Proxy مثل **NGINX یا Traefik** استفاده کنی، می‌تونی Load Balancing رو پیاده‌سازی کنی.

### 🔥 **مثال با NGINX به عنوان Load Balancer**
فرض کن دو تا کانتینر Nginx داری و می‌خوای از یه کانتینر سوم به عنوان Load Balancer استفاده کنی.

```bash
docker network create my-lb-network
```

```bash
docker run -d --name web1 --network my-lb-network nginx
docker run -d --name web2 --network my-lb-network nginx
```

حالا یه فایل کانفیگ برای NGINX به اسم `nginx.conf` درست کن:

```nginx
http {
    upstream myapp {
        server web1;
        server web2;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://myapp;
        }
    }
}
```

حالا NGINX رو به عنوان Load Balancer اجرا کن:

```bash
docker run -d --name lb --network my-lb-network -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro -p 8080:80 nginx
```

✅ حالا اگه بری به آدرس `http://localhost:8080` و چند بار Refresh کنی، می‌بینی که به نوبت به `web1` و `web2` وصل می‌شه! 🎉

