<h1 id="WMS" dir="rtl">WMS</h1>

<p dir="rtl">در این بخش به توضیحات سرویس  <a href="https://docs.geoserver.org/2.22.x/en/user/services/wms/reference.html">WMS</a> می پردازیم. </p>

<h2 id="-" dir="rtl">تعریف</h2>
<p dir="rtl">WMS خلاصه شده‌ی web map service می‌باشد.</p>
<p dir="rtl">کاربرد های سرویس WMS :</p>
<ol dir="rtl">
<li dir="rtl">دریافت لیست لایه های در دسترس</li>
<li dir="rtl">دریافت تصاویر لایه برای نمایش روی نقشه</li>
<li dir="rtl">برداشت اطلاعات از نقشه</li>
<li dir="rtl">دریافت نمای کوچک قالب</li>
</ol>

<h2 id="-" dir="rtl">عملیات های قابل پشتیبانی</h2>
<p dir="rtl">در تصویر زیر تمامی عملیات های قابل پشتیبانی توسط سرویس WMS را مشاهده می‌کنیم.</p>
<p dir="ltr"  style="background-color: mistyrose"><img src="https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/wms-oprations.png" alt="WMS supported operations" title="WMS supported operations"></p>

<ol dir="rtl">
    <li dir="rtl">GetCapabilities
    <ol dir="rtl" style="list-style: none">
    <li dir="rtl" style="list-style: none"><p dir="rtl">فرا داده‌ای مربوط به سرویس مانند لیست لایه ها، پارامتر ها و عملیات های قابل پشتیبانی را در خروجی می‌دهد.</p></li>
    </ol>
    </li>
    <li dir="rtl">GetMap
    <ol dir="rtl" style="list-style: none">
    <li dir="rtl" style="list-style: none"><p dir="rtl">یک تصویر نقشه را بر می‌گرداند.</p></li>
    </ol>
    </li>
    <li dir="rtl">GetFeatureInfo
    <ol dir="rtl" style="list-style: none">
    <li dir="rtl" style="list-style: none"><p dir="rtl">داده‌های لایه را براساس یک پیکسل نقشه باز می‌گرداند.</p></li>
    </ol>
    </li>
    <li dir="rtl">DescribeLayer
    <ol dir="rtl" style="list-style: none">
    <li dir="rtl" style="list-style: none"><p dir="rtl">آدرس سرویس WFS یا WCS برای دریافت اطلاعات بیشتر در مورد لایه را می‌دهد. </p></li>
    </ol>
    </li>
    <li dir="rtl">GetLegendGraphic
    <ol dir="rtl" style="list-style: none">
    <li dir="rtl" style="list-style: none"><p dir="rtl">نمای کوچک قالب را باز می‌گرداند.</p></li>
    </ol>
    </li>
</ol>

<h2 id="-" dir="rtl">استفاده از سرویس WMS سامانه ژئوتاژک</h2>

<ol dir="rtl">

<p dir="rtl">توجه داشته باشیدقبل از استفاده از مثال های این بخش باید از کارشناس سامانه درخواست Apikey و آدرس سرویس WMS را بدهید.</p>

<li dir="rtl">استفاده در نرم‌افزار QGIS</li>
<p dir="ltr"  style="background-color: mistyrose"><img src="https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/add-wms-qgis.png" alt="add WMS to qgis" title="add WMS to qgis"></p>
<p dir="rtl">مطابق تصویر بالا آدرس WMS را در قسمت URL قرار می‌دهیم و در ادامه گزینه های چشم پوشی آدرس گزارش شده در GetCapabilities را نیز انتخاب می‌کنیم.</p>
<p dir="rtl">دلیل انتخاب گزینه چشم پوشی آدرس های گزارش شده در GetCapabilities این است که درون خروجی GetCapabilities آدرس های اورده شده آدرس های داخلی می‌باشد و چون ما به آن ها دسترسی نداریم این گزینه ها را انتخاب می‌کنیم.</p>
</ol>