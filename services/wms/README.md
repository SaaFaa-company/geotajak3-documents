# سرویس WMS
در این بخش به توضیحات سرویس WMS می‌پردازیم.

### تعریف
سرویس WMS خلاصه شده‌ی Web Map Service می‌باشد.

کاربرد های سرویس WMS

- دریافت لیست لایه های در دسترس
- دریافت تصاویر لایه برای نمایش روی نقشه
- برداشت اطلاعات از نقشه
- دریافت نمای کوچک قالب

### عملیات های قابل پشتیبانی
در تصویر زیر تمامی عملیات های قابل پشتیبانی توسط سرویس WMS را مشاهده می‌کنیم.

![WMS supported operations!](https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/wms-oprations.png "WMS supported operations")

- عملیات GetCapabilities
  - فرا داده‌ای مربوط به سرویس مانند لیست لایه ها، پارامتر ها و عملیات های قابل پشتیبانی را در خروجی می‌دهد
- عملیات GetMap
  - یک تصویر نقشه را بر می‌گرداند.
- عملیات GetFeatureInfo
  - داده‌های لایه را براساس یک پیکسل نقشه باز می‌گرداند.
- عملیات DescribeLayer
  - آدرس سرویس WFS یا WCS برای دریافت اطلاعات بیشتر در مورد لایه را می‌دهد.
- عملیات GetLegendGraphic
  - نمای کوچک قالب را باز می‌گرداند.
  
## استفاده از سرویس WMS سامانه ژئوتاژک

توجه داشته باشیدقبل از استفاده از مثال های این بخش باید از کارشناس سامانه درخواست Apikey و آدرس سرویس WMS را بدهید.

- استفاده در نرم‌افزار QGIS
  - ![add WMS to qgis!](https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/add-wms-qgis.png "add WMS to qgis")
    - مطابق تصویر بالا آدرس WMS را در قسمت URL قرار می‌دهیم و در ادامه گزینه های چشم پوشی آدرس گزارش شده در GetCapabilities را نیز انتخاب می‌کنیم.
    - دلیل انتخاب گزینه چشم پوشی آدرس های گزارش شده در GetCapabilities این است که درون خروجی GetCapabilities آدرس های اورده شده آدرس های داخلی می‌باشد و چون ما به آن ها دسترسی نداریم این گزینه ها را انتخاب می‌کنیم.
    
- با استفاده از request
  - عملیات GetCapabilities
    - ```
        curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/{your apikey}/wms/?service=wms&version=1.1.1&request=GetCapabilities'
      ```
      - {your apikey} : کلید دسترسی که از کارشناس سامانه دریافت می کنید
  - عملیات GetMap
    - ```
        curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/{your apikey}/wms/?service=wms&version=1.3.0&request=GetMap&layers={layer name}&FORMAT=image/png&height=256&width=256&bbox={bbox}&CRS={crs}&srs={srs}&TILED=true&STYLES={style name}'
      ```
      - {layer name} : نام لایه مورد نظر در ژئوسرور
      - {bbox} : محدوده مورد نظر
      - {src} : پروژکشنی که تایل نقشه براساس آن ساخته شود
      - {crs} : پروژکشنی که تایل نقشه براساس آن ساخته شود
      - {style name} : نام استایلی که ژئوسرور برای ساخت تایل استفاده کند
  - عملیات GetFeatureInfo
    - ```
        curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/{your apikey}/wms/?service=wms&version=1.3.0&request=GetFeatureInfo&layers={layer name}&info_format=application/json&height=256&width=256&bbox={bbox}&CRS={crs}6&srs={srs}&STYLES={style name}&QUERY_LAYERS={layer name}&FEATURE_COUNT=50&I={i}&J={j}'
      ```
      - {i} : نقطه ی مورد نظر بر اساس محور افقی برحسب پیکسل (0 نقطه سمت چپ)
      - {j} : نقطه ی مورد نظر براساس محور عمودی برحسب پیکسی (0 نقطه بالا)

- استفاده در کد javascript

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;برای استفاده از سرویس های OGC در کد جاوا اسکریپت به صورتی که بتوانیم لایه را در محیط وب مشاهده کنیم و عملیات های مورد نظر را بر روی آن انجام دهیم از کتابخانه‌ی open layer استفاده می‌کنیم.