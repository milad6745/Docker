برای نوشتن یک `Dockerfile` که شامل تمام گزینه‌های ممکن باشد و به‌عنوان یک مثال جامع عمل کند، می‌توان از موارد مختلف استفاده کرد. این نمونه یک وب اپلیکیشن ساده Python Flask را با در نظر گرفتن تمامی گزینه‌ها پوشش می‌دهد:

```dockerfile
# 1. Base Image
FROM python:3.11-slim

# 2. Maintainer Info
LABEL maintainer="your_email@example.com" \
      version="1.0" \
      description="A comprehensive example of Dockerfile options"

# 3. Set Environment Variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    APP_HOME=/app

# 4. Working Directory
WORKDIR $APP_HOME

# 5. Copy Local Files
COPY . $APP_HOME

# 6. Update and Install System Packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl \
    netcat && \
    rm -rf /var/lib/apt/lists/*

# 7. Install Python Dependencies
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# 8. Expose Application Port
EXPOSE 5000

# 9. Define Volumes
VOLUME ["/app/static", "/app/media"]

# 10. Health Check
HEALTHCHECK --interval=30s --timeout=5s --retries=3 CMD curl -f http://localhost:5000/ || exit 1

# 11. Set Default User
RUN useradd -m flaskuser
USER flaskuser

# 12. Command to Run Application
CMD ["python", "app.py"]
```

---

### **توضیح گزینه‌ها**
1. **`FROM`: تصویر پایه**  
   این دستور تصویر پایه را مشخص می‌کند، در اینجا از `python:3.11-slim` استفاده شده است.

2. **`LABEL`: افزودن اطلاعات متا**  
   برای مشخص کردن اطلاعاتی مانند نگهدارنده، نسخه و توضیحات.

3. **`ENV`: تعریف متغیرهای محیطی**  
   متغیرهایی برای کنترل رفتار برنامه یا محیط (مثلاً غیرفعال کردن تولید فایل‌های `.pyc`).

4. **`WORKDIR`: دایرکتوری کاری داخل کانتینر**  
   تمامی دستورات پس از این در مسیر `/app` اجرا خواهند شد.

5. **`COPY`: کپی فایل‌های محلی**  
   فایل‌های پروژه به داخل کانتینر کپی می‌شوند.

6. **`RUN`: اجرای دستورات در زمان ساخت**  
   نصب بسته‌های سیستمی و پایتونی. همچنین پاک کردن کش برای کاهش حجم تصویر.

7. **`EXPOSE`: مشخص کردن پورت**  
   این دستور مشخص می‌کند که اپلیکیشن روی پورت 5000 اجرا خواهد شد.

8. **`VOLUME`: تعریف دایرکتوری‌های دائمی**  
   دایرکتوری‌هایی که می‌توانند خارج از کانتینر ذخیره شوند.

9. **`HEALTHCHECK`: بررسی سلامت کانتینر**  
   تست وضعیت سرویس به‌صورت دوره‌ای.

10. **`USER`: تغییر کاربر پیش‌فرض**  
    برای افزایش امنیت، از یک کاربر غیر ریشه (root) استفاده شده است.

11. **`CMD`: اجرای دستور اصلی**  
    مشخص می‌کند که کانتینر چه کاری باید انجام دهد. در اینجا اپلیکیشن Flask اجرا می‌شود.

---
