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

<li dir="rtl">با استفاده از request</li>
<h5 dir="rtl">GetCapabilities</h5>
<p dir="rtl">
<code dir="ltr">
curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzc0MDY3NzA2LCJqdGkiOiJjNTUzYWQ2ZTEwYmE0ZWQ1YmFkNWUxZGExZGNkY2FmMiIsInVzZXJfaWQiOjYwLCJkZXYiOiJhcGkiLCJ1c2VybmFtZSI6ImRvYyJ9.7KDeaHIzrGj0Nba8vbNWbAhUSjrFP61zTK4OlVV5sKE/wms/?service=wms&version=1.1.1&request=GetCapabilities'
</code></p>
<h5 dir="rtl">GetMap</h5>
<p dir="rtl">
<code dir="ltr">
curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzc0MDY3NzA2LCJqdGkiOiJjNTUzYWQ2ZTEwYmE0ZWQ1YmFkNWUxZGExZGNkY2FmMiIsInVzZXJfaWQiOjYwLCJkZXYiOiJhcGkiLCJ1c2VybmFtZSI6ImRvYyJ9.7KDeaHIzrGj0Nba8vbNWbAhUSjrFP61zTK4OlVV5sKE/wms/?service=wms&version=1.3.0&request=GetMap&layers=geotajak:shahrestan_100_new&FORMAT=image/png&height=256&width=256&bbox=33.75,56.25,39.375,61.875&CRS=EPSG:4326&srs=EPSG:4326&TILED=true&STYLES=shahrestan_100_new_89_initial'
</code></p>
<h5 dir="rtl">GetFeatureInfo</h5>
<p dir="rtl">
<code dir="ltr">
curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzc0MDY3NzA2LCJqdGkiOiJjNTUzYWQ2ZTEwYmE0ZWQ1YmFkNWUxZGExZGNkY2FmMiIsInVzZXJfaWQiOjYwLCJkZXYiOiJhcGkiLCJ1c2VybmFtZSI6ImRvYyJ9.7KDeaHIzrGj0Nba8vbNWbAhUSjrFP61zTK4OlVV5sKE/wms/?service=wms&version=1.3.0&request=GetFeatureInfo&layers=geotajak:shahrestan_100_new&FORMAT=image/png&height=256&width=256&bbox=28.125,50.625,33.75,56.25&CRS=EPSG:4326&srs=EPSG:4326&STYLES=shahrestan_100_new_89_initial&QUERY_LAYERS=geotajak:shahrestan_100_new&FEATURE_COUNT=50&I=212&J=45'
</code></p>

</ol>