## Hello World

معمولا عبارت "Hello World" مثالی از اولین قدم برای یادگیری یک زبان جدید است.

در مورد ما ارائه یک متن کار پیچیده ای برای قدم اول است، در عوض یک رنگ روشن را به عنوان شور و شوق اولین کدمان اجرا می‌کنیم!

<div class="codeAndCanvas" data="hello_world.frag"></div>

اگر این کتاب را در یک مرورگر مدرن می‌خوانید، کد بالا قابل تغییر است، تغییرات شما بلافاصله کامپایل و به شما نمایش داده می‌شوند، سعی کنید خط 8 را تغییر دهید.

البته این خطوط ساده به نظر نمی‌رسند، اما می‌توان مفاهیم قابل توجهی از آنها استباط کرد:

1. برنامه نویسی شیدر یک عملکرد اصلی 'main' دارد، که در انتها یک رنگ برمی‌گرداند. شبیه زبان C.

2. رنگ نهایی پیکسل به متغیر گلوبال gl_FragColor اختصاص داده شده است.

3. این زبان شبه C با متغیر ها و تابع های مختلف ساخته شده و استفاده می‌شود. در این مورد ما با vect4 آشنا شدیم که مخفف یک بردار 4 بعدی با دقت شناور(float) است. انواع بیشتری ازین متغیر ها مانند vect2, vect3 و bool, int, float در آینده خواهیم دید.

4. اگر به vect4 دقت کنیم می‌یابیم این 4 آرگومان به کانال های RGBA پیکسل مورد نظر پاسخ می‌دهند. همچنین این مقادیر نرمال شده اند یعنی بین 0تا1(نه بین 0 تا 255)، بعدا خواهیم آموخت چگونه نرمال سازی مقادیر، ترسیم مقادیر بین متغیر ها را آسان می‌کند.

5. یکی از دیگر ویژگی های مشابه C مثال بالا وجود ماکرو ها هستند. با استفاده از آنان می‌توان متغیر های جهانی را تعریف کرد و یا برخی عملیات شرطی اساسی را انجام داد(ifdef and #endif#). تمام دستورات کلان(ماکرو) با هشتگ شروع می‌شوند. ماکرو ها قبل از کامپایل اجرا می‌شوند، شرایط را بررسی می‌کند(ifdef and #endif#) و ارجاعات به defines# را کپی می‌کند. مثلا در مثال بالا ما خط 2 را در صورت تعریف GL_ES وارد می‌کنیم. که معمولا در هنگام کامپایل این کد در تلفن های همراه و مرورگر ها اتفاق می‌افتد.

6. شناور ها(float) در شیدر ها حیاتی هستند، بنابراین سطح دقت بسیار مهم است. دقت پایین تر به معنای رندر سریع تر است، همچنین کیفیت کمتر. می‌توانید مثل من خط دو مثال بالا متغیر ها را شناور با دقت متوسط درنظر بگیرید(precision mediump float)، همچنین می‌توانید متغیر شناور با دقت پایین(precision lowp float) یا بالا(precision highp float)هم در نظر بگیرید.

7. آخرین و شاید مهمترین نکته در مثال بالا اینکه در GLSL تضمین نمی‌شود که متغیر ها به طور خودکار تغییر نوع داده(casting) رویشان اعمال شود. این به چه معناست؟ تولید کنندگان رویکرد های مختلفی برای سرعت بخشیدن روند پردازش کارت های گرافیکی دارند، و مجبورند حداقل مشخصات را تضمین کنند. کستینگ ازین رویکرد ها نیست. در مثال بالا vect4 دارای نقطه شناور است و برای آن انتظار می‌رود که به متغیر های شناور انتساب شود. اگر می‌خواهید کد سازگار خوبی ایجاد کنید و ساعت ها وقت صرف دیبگ کردن آن نکنید، عادت کنید در float ها از نقطه(.) استفاده کنید.

```glsl
void main() {
    gl_FragColor = vec4(1,0,0,1);	// ERROR
}
```

اکنون که مهم ترین عناصر مثال بالا را با هم مرور کردیم، وقت آن است که روی کد کلیک کنید و چیز هایی که یاد گرفتیم را پیاده کنیم. توجه کنید که در صورت خطا برنامه صفحه سفید را به شما نشان می‌دهد. بعضی چیز های جالب وجود دارد که باید امتحان کنید، مثلا:

* شناور ها را با اعداد صحیح(int) جایگزین کنید، کارت گرافیک شما معلوم نیست بتواند این کد را اجرا کند یا خیر.

* سعی کنید خط 8 را کامنت کنید و هیچ مقدار پیکسلی به تابع اختصاص ندهید.

* سعی کنید یک تابع جداگانه ایجاد کنید که رنگ خاصی را برگرداند و از آن داخل main استفاده کنید، به عنوان یک راهنمایی در اینجا کد مربوط به تابعیست که رنگ قرمز را بر می‌گرداند.

```glsl
vec4 red(){
    return vec4(1.0,0.0,0.0,1.0);
}
```

* روش ها مختلفی برای ساخت vect4 وجود دارد، سعی کنید راه های دیگر را پیدا کنید، یکی از آن ها به این صورت است:

```glsl
vec4 color = vec4(vec3(1.0,0.0,1.0),1.0);
```

اگرچه این مثال خیلی هیجان انگیز نیست، اما ابتدایی ترین مثال است. ما تمام پیکسل های داخل کنوس(canvas) را به یک رنگ تغییر می‌دهیم. در فصل بعد نحوه تغییر رنگ پیکسل را با استفاده از دو نوع ورودی دیگر می‌بینیم. فضا(محل و مختصات پیکسل روی صفحه) و زمان(مقدار زمان از لحظه بارگیری صفحه بر حسب ثانیه).
