سلام!
مفهوم **Docker multi-stage build** برای ساختن imageهای کوچک‌تر، تمیزتر و ایزوله‌تر استفاده می‌شه. به‌طور خلاصه، در multi-stage build شما می‌تونید چند مرحله ساخت (stage) در یک Dockerfile تعریف کنید. معمولاً در یک مرحله برنامه‌تون رو build می‌کنید (که ممکنه ابزارها و پکیج‌های زیادی لازم داشته باشه)، و در مرحله‌ی بعد فقط خروجی نهایی رو در یک image سبک‌تر کپی می‌کنید.

---

### مثال ساده:

فرض کن یک برنامه Go داری:

```dockerfile
# مرحله اول: ساخت برنامه
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# مرحله دوم: اجرای برنامه
FROM debian:bookworm-slim
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

---

### مزایای Multi-stage:

* حجم نهایی image بسیار کمتره
* ابزارها و dependencyهایی که فقط برای build نیازن، وارد image نهایی نمی‌شن
* امنیت و سرعت deploy بالاتر می‌ره

---

