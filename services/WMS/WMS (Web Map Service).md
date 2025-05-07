
## مقدمه

سرویس WMS (Web Map Service) یکی از استانداردهای اصلی [OGC](https://www.ogc.org/) (Open Geospatial Consortium) برای ارائه نقشه‌های جغرافیایی به صورت تصویر در محیط وب است. این سرویس امکان درخواست و دریافت داده‌های مکانی را به صورت تصویری فراهم می‌کند.

## تعریف

WMS مخفف Web Map Service می‌باشد. این سرویس استانداردی است که توسط OGC تعریف شده و به کاربران اجازه می‌دهد تا نقشه‌های مکانی را به صورت تصویر در فرمت‌هایی مانند PNG، JPEG یا GIF دریافت کنند.

## کاربردهای سرویس WMS

سرویس WMS کاربردهای متعددی دارد، از جمله:

- **دریافت لیست لایه‌های در دسترس**: امکان مشاهده تمامی لایه‌های موجود در سرویس
- **دریافت تصاویر لایه برای نمایش روی نقشه**: امکان نمایش داده‌های مکانی به صورت تصویر
- **برداشت اطلاعات از نقشه**: امکان استخراج اطلاعات از نقاط مختلف نقشه
- **دریافت نمای کوچک قالب (Legend)**: امکان دریافت راهنمای نقشه برای نمایش به کاربر

## عملیات‌های قابل پشتیبانی

WMS از عملیات‌های متعددی پشتیبانی می‌کند که در تصویر زیر قابل مشاهده هستند:

![WMS supported operations](https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/wms-oprations.png "WMS supported operations")

### عملیات GetCapabilities

این عملیات فراداده‌های مربوط به سرویس را ارائه می‌دهد، شامل:

- لیست لایه‌های موجود
- پارامترهای قابل استفاده
- عملیات‌های قابل پشتیبانی
- سیستم‌های مختصات پشتیبانی شده
- محدوده جغرافیایی داده‌ها

پاسخ این درخواست معمولاً در قالب XML ارائه می‌شود و شامل اطلاعات کاملی در مورد قابلیت‌های سرویس است.

### عملیات GetMap

این عملیات یک تصویر نقشه را مطابق با پارامترهای درخواست شده برمی‌گرداند. پارامترهای اصلی این عملیات عبارتند از:

- نام لایه یا لایه‌ها (LAYERS)
- سیستم مختصات (CRS یا SRS)
- محدوده جغرافیایی (BBOX)
- ابعاد تصویر (WIDTH و HEIGHT)
- فرمت خروجی (FORMAT)
- استایل نمایش (STYLES)

### عملیات GetFeatureInfo

این عملیات امکان استخراج اطلاعات توصیفی اشیاء موجود در نقشه را بر اساس موقعیت یک پیکسل فراهم می‌کند. این قابلیت به کاربران اجازه می‌دهد با کلیک بر روی نقشه، اطلاعات مربوط به آن نقطه را دریافت کنند.

پارامترهای اصلی این عملیات عبارتند از:

- نام لایه یا لایه‌ها (QUERY_LAYERS)
- موقعیت پیکسل (I و J)
- فرمت خروجی (INFO_FORMAT)
- تعداد عوارض مورد نظر (FEATURE_COUNT)

### عملیات DescribeLayer

این عملیات آدرس سرویس‌های WFS یا WCS مرتبط با لایه را برای دریافت اطلاعات بیشتر در مورد لایه ارائه می‌دهد. این عملیات برای ارتباط بین سرویس‌های مختلف OGC مفید است.

### عملیات GetLegendGraphic

این عملیات تصویری از راهنمای نقشه (Legend) را برای یک لایه یا استایل خاص برمی‌گرداند. این تصویر معمولاً شامل نمادها و رنگ‌های استفاده شده در نقشه به همراه توضیحات آن‌ها است.

## استفاده از سرویس WMS سامانه ژئوتاژک

**نکته مهم**: قبل از استفاده از مثال‌های این بخش، باید از کارشناس سامانه درخواست Apikey و آدرس سرویس WMS را داشته باشید.

### استفاده در نرم‌افزار QGIS

QGIS یکی از نرم‌افزارهای مشهور GIS است که از سرویس WMS پشتیبانی می‌کند. برای اضافه کردن سرویس WMS به QGIS:

1. از منوی لایه (Layer) گزینه "Add WMS/WMTS Layer" را انتخاب کنید
2. بر روی دکمه "New" کلیک کنید تا یک اتصال جدید ایجاد کنید
3. نام و آدرس سرویس WMS را وارد کنید
4. مطابق تصویر زیر، آدرس WMS را در قسمت URL قرار دهید:

![add WMS to qgis](https://raw.githubusercontent.com/SaaFaa-company/geotajak3-documents/main/services/image/add-wms-qgis.png "add WMS to qgis")

5. گزینه‌های "Ignore GetMap/GetTile URI reported in capabilities" و "Ignore GetFeatureInfo URI reported in capabilities" را انتخاب کنید

**توضیح مهم**: دلیل انتخاب گزینه‌های چشم‌پوشی از آدرس‌های گزارش شده در GetCapabilities این است که در خروجی GetCapabilities، آدرس‌های ارائه شده آدرس‌های داخلی هستند و چون ما به آن‌ها دسترسی نداریم، این گزینه‌ها را انتخاب می‌کنیم.

### استفاده با درخواست‌های HTTP (curl)

#### عملیات GetCapabilities

برای دریافت اطلاعات کامل در مورد سرویس و لایه‌های موجود:

```bash
curl --location --request GET 'http://{your_ip}/api/proxy/api_key/{your_apikey}/wms/?service=wms&version=1.1.1&request=GetCapabilities'
```

**پارامترها**:

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر

**پارامترهای درخواست**:

- `service=wms`: نوع سرویس مورد درخواست (WMS)
- `version=1.1.1`: نسخه پروتکل WMS
- `request=GetCapabilities`: نوع عملیات درخواستی

#### عملیات GetMap

برای دریافت تصویر نقشه:

```bash
curl --location --request GET 'http://{your_ip}/api/proxy/api_key/{your_apikey}/wms/?service=wms&version=1.3.0&request=GetMap&layers={layer_name}&FORMAT=image/png&height=256&width=256&bbox={bbox}&CRS={crs}&srs={srs}&TILED=true&STYLES={style_name}'
```

**پارامترها**:

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر
- `{layer_name}`: نام لایه مورد نظر در ژئوسرور
- `{bbox}`: محدوده جغرافیایی مورد نظر (مثال: `51.3,35.6,51.5,35.8`)
- `{srs}`: سیستم مختصات مورد استفاده (مثال: `EPSG:4326`)
- `{crs}`: سیستم مختصات مورد استفاده (مثال: `EPSG:4326`)
- `{style_name}`: نام استایلی که ژئوسرور برای ساخت تایل استفاده می‌کند

**پارامترهای درخواست**:

- `service=wms`: نوع سرویس مورد درخواست (WMS)
- `version=1.3.0`: نسخه پروتکل WMS
- `request=GetMap`: نوع عملیات درخواستی
- `FORMAT=image/png`: فرمت تصویر خروجی
- `height=256`: ارتفاع تصویر به پیکسل
- `width=256`: عرض تصویر به پیکسل
- `TILED=true`: درخواست تایل‌بندی شده

#### عملیات GetFeatureInfo

برای دریافت اطلاعات یک نقطه خاص از نقشه:

```bash
curl --location --request GET 'http://{your_ip}/api/proxy/api_key/{your_apikey}/wms/?service=wms&version=1.3.0&request=GetFeatureInfo&layers={layer_name}&info_format=application/json&height=256&width=256&bbox={bbox}&CRS={crs}&srs={srs}&STYLES={style_name}&QUERY_LAYERS={layer_name}&FEATURE_COUNT=50&I={i}&J={j}'
```

**پارامترها**:

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر
- `{layer_name}`: نام لایه مورد نظر در ژئوسرور
- `{bbox}`: محدوده جغرافیایی مورد نظر
- `{srs}`: سیستم مختصات مورد استفاده
- `{crs}`: سیستم مختصات مورد استفاده
- `{style_name}`: نام استایل مورد استفاده
- `{i}`: نقطه مورد نظر بر اساس محور افقی برحسب پیکسل (0 نقطه سمت چپ)
- `{j}`: نقطه مورد نظر بر اساس محور عمودی برحسب پیکسل (0 نقطه بالا)

**پارامترهای درخواست**:

- `service=wms`: نوع سرویس مورد درخواست (WMS)
- `version=1.3.0`: نسخه پروتکل WMS
- `request=GetFeatureInfo`: نوع عملیات درخواستی
- `info_format=application/json`: فرمت خروجی اطلاعات
- `height=256`: ارتفاع تصویر به پیکسل
- `width=256`: عرض تصویر به پیکسل
- `QUERY_LAYERS={layer_name}`: لایه مورد پرس و جو
- `FEATURE_COUNT=50`: حداکثر تعداد عوارض بازگشتی

### استفاده در کد JavaScript

برای استفاده از سرویس‌های OGC در کد جاوا اسکریپت به صورتی که بتوانیم لایه را در محیط وب مشاهده کنیم و عملیات‌های مورد نظر را بر روی آن انجام دهیم، از کتابخانه [OpenLayers](https://openlayers.org/) استفاده می‌کنیم.

در ادامه مثال‌هایی از استفاده OpenLayers برای نمایش لایه‌های WMS و برداشت اطلاعات ارائه شده است:

#### مثال 1: نمایش لایه WMS

```html
<!DOCTYPE html>
<html>
<head>
  <title>نمایش لایه WMS</title>
  <meta charset="utf-8">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ol@v7.3.0/ol.css">
  <script src="https://cdn.jsdelivr.net/npm/ol@v7.3.0/dist/ol.js"></script>
  <style>
    #map {
      width: 100%;
      height: 500px;
    }
  </style>
</head>
<body>
  <div id="map"></div>
  <script>
    // تعریف منبع لایه WMS
    const wmsSource = new ol.source.TileWMS({
      url: 'http://{your_ip}/api/proxy/api_key/{your_apikey}/wms/',
      params: {
        'LAYERS': '{layer_name}',
        'TILED': true,
        'VERSION': '1.3.0',
        'FORMAT': 'image/png',
        'STYLES': '{style_name}'
      },
      serverType: 'geoserver',
      crossOrigin: 'anonymous'
    });

    // تعریف لایه
    const wmsLayer = new ol.layer.Tile({
      source: wmsSource,
      visible: true,
      title: 'WMS Layer'
    });

    // تعریف نقشه
    const map = new ol.Map({
      target: 'map',
      layers: [
        // لایه پایه OpenStreetMap
        new ol.layer.Tile({
          source: new ol.source.OSM(),
          visible: true,
          title: 'OSM'
        }),
        // لایه WMS
        wmsLayer
      ],
      view: new ol.View({
        center: ol.proj.fromLonLat([51.4, 35.7]), // مرکز نقشه (تهران)
        zoom: 10
      })
    });
  </script>
</body>
</html>
```

#### مثال 2: برداشت اطلاعات از لایه WMS

```html
<!DOCTYPE html>
<html>
<head>
  <title>برداشت اطلاعات از لایه WMS</title>
  <meta charset="utf-8">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ol@v7.3.0/ol.css">
  <script src="https://cdn.jsdelivr.net/npm/ol@v7.3.0/dist/ol.js"></script>
  <style>
    #map {
      width: 100%;
      height: 500px;
    }
    #info {
      position: absolute;
      height: 200px;
      width: 300px;
      background-color: white;
      border: 1px solid #ccc;
      padding: 10px;
      overflow: auto;
      display: none;
    }
  </style>
</head>
<body>
  <div id="map"></div>
  <div id="info"></div>
  <script>
    // تعریف منبع لایه WMS
    const wmsSource = new ol.source.TileWMS({
      url: 'http://{your_ip}/api/proxy/api_key/{your_apikey}/wms/',
      params: {
        'LAYERS': '{layer_name}',
        'TILED': true,
        'VERSION': '1.3.0',
        'FORMAT': 'image/png',
        'STYLES': '{style_name}'
      },
      serverType: 'geoserver',
      crossOrigin: 'anonymous'
    });

    // تعریف لایه
    const wmsLayer = new ol.layer.Tile({
      source: wmsSource,
      visible: true,
      title: 'WMS Layer'
    });

    // تعریف نقشه
    const map = new ol.Map({
      target: 'map',
      layers: [
        // لایه پایه OpenStreetMap
        new ol.layer.Tile({
          source: new ol.source.OSM(),
          visible: true,
          title: 'OSM'
        }),
        // لایه WMS
        wmsLayer
      ],
      view: new ol.View({
        center: ol.proj.fromLonLat([51.4, 35.7]), // مرکز نقشه (تهران)
        zoom: 10
      })
    });

    // برداشت اطلاعات با کلیک روی نقشه
    map.on('singleclick', function(evt) {
      const viewResolution = map.getView().getResolution();
      const url = wmsSource.getFeatureInfoUrl(
        evt.coordinate,
        viewResolution,
        'EPSG:3857',
        {
          'INFO_FORMAT': 'application/json',
          'FEATURE_COUNT': 50,
          'QUERY_LAYERS': '{layer_name}'
        }
      );

      if (url) {
        fetch(url)
          .then(response => response.json())
          .then(data => {
            const infoDiv = document.getElementById('info');
            if (data.features && data.features.length > 0) {
              // نمایش اطلاعات
              infoDiv.style.display = 'block';
              infoDiv.style.left = (evt.pixel[0] + 10) + 'px';
              infoDiv.style.top = (evt.pixel[1] + 10) + 'px';
              
              let content = '<h4>اطلاعات عارضه</h4>';
              const properties = data.features[0].properties;
              for (const property in properties) {
                content += `<p><strong>${property}:</strong> ${properties[property]}</p>`;
              }
              infoDiv.innerHTML = content;
            } else {
              infoDiv.style.display = 'none';
            }
          });
      }
    });

    // بستن پنجره اطلاعات با کلیک در جای دیگر
    map.on('click', function(evt) {
      const infoDiv = document.getElementById('info');
      if (!infoDiv.contains(evt.target)) {
        infoDiv.style.display = 'none';
      }
    });
  </script>
</body>
</html>
```

## نکات تکمیلی

- در سرویس‌های WMS، حجم داده‌ها می‌تواند بسیار زیاد باشد، بنابراین استفاده از پارامترهایی مانند `TILED=true` برای بهینه‌سازی عملکرد توصیه می‌شود.
- سیستم مختصات در نسخه‌های مختلف WMS متفاوت است. در نسخه 1.1.1 از پارامتر `SRS` و در نسخه 1.3.0 از پارامتر `CRS` استفاده می‌شود.
- در نسخه 1.3.0، ترتیب مختصات در `BBOX` برعکس نسخه 1.1.1 است (در EPSG:4326، ابتدا عرض جغرافیایی و سپس طول جغرافیایی).
- هنگام استفاده از OpenLayers، مراقب تبدیل سیستم‌های مختصات باشید. OpenLayers به طور پیش‌فرض از EPSG:3857 استفاده می‌کند، اما بسیاری از داده‌های WMS در EPSG:4326 هستند.

## خطاهای رایج و روش‌های رفع آن‌ها

### خطای دسترسی (401 Unauthorized)

- **دلیل**: کلید API نامعتبر یا منقضی شده است.
- **راه حل**: با کارشناس سامانه برای دریافت کلید API معتبر تماس بگیرید.

### خطای عدم دسترسی به لایه (Layer not found)

- **دلیل**: نام لایه اشتباه وارد شده یا لایه در دسترس نیست.
- **راه حل**: با استفاده از عملیات GetCapabilities، لیست لایه‌های موجود را بررسی کنید.

### خطای عدم نمایش تصویر در محدوده مشخص (Empty image)

- **دلیل**: محدوده جغرافیایی (BBOX) خارج از محدوده لایه است یا داده‌ای در آن محدوده وجود ندارد.
- **راه حل**: با استفاده از عملیات GetCapabilities، محدوده قابل دسترس لایه را بررسی و تنظیم کنید.

## منابع تکمیلی

- [مستندات رسمی OGC برای WMS](https://www.ogc.org/standards/wms)
- [مستندات OpenLayers](https://openlayers.org/en/latest/apidoc/)
- [آموزش‌های GeoServer](https://docs.geoserver.org/)