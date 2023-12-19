دستورات `docker pull` و `docker push` به ترتیب برای دریافت تصویر از یک مخزن (pull) و ارسال تصویر به یک مخزن (push) در Docker استفاده می‌شوند. این دستورات به شما این امکان را می‌دهند که تصاویر Docker را به اشتراک بگذارید و از مخازن عمومی یا خصوصی مختلف دریافت و ارسال کنید.

### مثال `docker pull`:

```bash
docker pull ubuntu:latest
```

این دستور تصویر آخرین نسخه از سیستم‌عامل Ubuntu را از مخزن Docker Hub دریافت می‌کند. در اینجا:

- `ubuntu` نام مخزن تصویر (repository) است.
- `latest` برچسب (tag) تصویر است.

### مثال `docker push`:

فرض کنید شما یک تصویر سفارشی ایجاد کرده‌اید و می‌خواهید آن را به یک مخزن خصوصی خود ارسال کنید. ابتدا باید تصویر خود را با برچسب مخصوصی بسازید و سپس با دستور `docker push` آن را به مخزن ارسال کنید.

#### برچسب‌گذاری تصویر:

```bash
docker build -t my-custom-image:latest .
```

#### ارسال تصویر به مخزن:

```bash
docker push my-registry/my-custom-image:latest
```

در اینجا:

- `my-registry` نام مخزن خصوصی است.
- `my-custom-image` نام تصویر است.
- `latest` برچسب تصویر است.

برای استفاده از `docker push` برای مخازن عمومی مثل Docker Hub، شما باید لاگین به حساب کاربری Docker Hub خود را انجام دهید:

```bash
docker login
```

سپس وارد اطلاعات لاگین شما شده و سپس می‌توانید `docker push` را اجرا کنید.

```bash
docker push your-docker-id/my-custom-image:latest
```

دستورات `docker pull` و `docker push` به شما این امکان را می‌دهند تا تصاویر Docker خود را بین محیط‌ها به اشتراک بگذارید و از مخازن مرکزی یا خصوصی مختلف استفاده کنید.
