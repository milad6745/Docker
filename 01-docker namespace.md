در Docker، «namespace» یا فضای نام یک مکانیزم ایزوله‌سازی است که باعث می‌شود پروسه‌های مختلفی که در یک کانتینر اجرا می‌شوند، از دیگر پروسه‌های سیستم و همچنین از کانتینرهای دیگر جدا شوند. این کار امنیت و ثبات را در سیستم فراهم می‌کند. فضای نام‌های مختلف در Docker و لینوکس به این شکل هستند:

 **PID Namespace**:

این فضای نام پروسه‌ها را از یکدیگر جدا می‌کند، به طوری که پروسه‌های یک کانتینر نمی‌توانند پروسه‌های کانتینرهای دیگر را مشاهده یا به آن‌ها دسترسی داشته باشند.

 **Network Namespace**:

6   این فضای نام شبکه‌های جداگانه‌ای برای هر کانتینر ایجاد می‌کند و هر کانتینر آدرس IP، پورت‌ها و قوانین فایروال مخصوص به خود را دارد.

 **Mount Namespace**:

   این فضای نام، سیستم فایل کانتینرها را جدا می‌کند. هر کانتینر سیستم فایل خودش را دارد و تغییرات در آن تأثیری روی سیستم فایل کانتینرهای دیگر یا سیستم میزبان ندارد.

**IPC Namespace**:

  این فضای نام برای ایزوله کردن مکانیزم‌های ارتباط بین‌پردازه‌ای (Interprocess Communication) مانند صف‌های پیام و حافظه‌ی مشترک است. این امکان باعث می‌شود کانتینرها تنها بتوانند به IPCهای خود دسترسی داشته باشند.

 **User Namespace**:

   این فضای نام کاربرها را ایزوله می‌کند. با استفاده از این فضای نام، هر کانتینر می‌تواند کاربر و گروه‌های خود را داشته باشد که از کاربران دیگر کانتینرها و سیستم میزبان جدا هستند.

 **UTS Namespace**:

این فضای نام به کانتینر اجازه می‌دهد نام میزبان (hostname) و نام دامنه را به‌طور جداگانه تنظیم کند. به این ترتیب هر کانتینر می‌تواند نام میزبان مخصوص به خود را داشته باشد.

به طور کلی، فضای نام‌ها در Docker به کانتینرها اجازه می‌دهند به شکل ایزوله و امنی در یک سیستم واحد فعالیت کنند، بدون اینکه با پروسه‌ها و منابع دیگر تداخلی داشته باشند.
