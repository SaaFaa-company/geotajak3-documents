
## معرفی

سرویس WFS مخفف "Web Feature Service" است که استانداردی برای تبادل داده‌های مکانی بر بستر وب می‌باشد. این سرویس امکان دسترسی، مدیریت و دستکاری داده‌های وکتوری را فراهم می‌کند.

## قابلیت‌های کلیدی

سرویس WFS قابلیت‌های متعددی را برای کار با داده‌های جغرافیایی ارائه می‌دهد:

- **دریافت داده‌های لایه**: امکان دانلود و استفاده از داده‌های وکتوری لایه‌های مختلف
- **ویرایش داده‌های لایه**: انجام عملیات CRUD (ایجاد، خواندن، به‌روزرسانی و حذف) روی داده‌ها
- **دریافت مشخصات لایه**: دستیابی به اطلاعات ساختاری لایه مانند فیلدها، نوع داده‌ها و سایر متاداده‌ها

## عملیات‌های استاندارد WFS

سرویس WFS چندین عملیات استاندارد را پشتیبانی می‌کند که هر کدام کاربرد خاصی دارند:

![عملیات‌های پشتیبانی‌شده WFS](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/Images/wfs-oprations.png?raw=true "عملیات‌های پشتیبانی‌شده WFS")

### 1. عملیات GetCapabilities

این عملیات اطلاعات کلی درباره سرویس WFS ارائه می‌دهد:

- فراداده‌های مربوط به سرویس‌های قابل ارائه توسط سرور
- توصیف عملیات‌های پشتیبانی‌شده و پارامترهای معتبر
- لیست لایه‌های در دسترس و مشخصات آنها

### 2. عملیات DescribeFeatureType

این عملیات ساختار داده‌ای لایه‌های درخواستی را توصیف می‌کند:

- اطلاعات مربوط به فیلدهای موجود در لایه
- نوع داده هر فیلد (عددی، متنی، تاریخ و غیره)
- محدودیت‌ها و قوانین مرتبط با داده‌ها

### 3. عملیات GetFeature

این عملیات اصلی‌ترین کارکرد WFS است که امکان دریافت داده‌های لایه را فراهم می‌کند:

- بازگرداندن داده‌های لایه در قالب‌های استاندارد (معمولاً GML یا GeoJSON)
- امکان اعمال فیلترهای مختلف برای دریافت داده‌های خاص
- قابلیت محدود کردن نتایج براساس معیارهای مکانی یا توصیفی

### 4. عملیات Transaction

این عملیات امکان تغییر داده‌های لایه را فراهم می‌کند:

- افزودن عوارض جدید
- ویرایش عوارض موجود
- حذف عوارض از لایه

## استفاده از سرویس WFS سامانه ژئوتاژک

> **نکته مهم**: برای استفاده از مثال‌های این بخش، باید از کارشناس سامانه درخواست API Key و آدرس سرویس WFS را داشته باشید.

### استفاده در نرم‌افزار QGIS

![افزودن WFS به QGIS](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/Images/add-wfs-qgis.png?raw=true "افزودن WFS به QGIS")

مراحل اتصال:

1. از منوی `لایه` گزینه `افزودن لایه` و سپس `افزودن لایه WFS` را انتخاب کنید
2. در پنجره باز شده، روی دکمه `جدید` کلیک کنید
3. نام اتصال دلخواه را وارد کنید
4. آدرس WFS دریافتی از کارشناس سامانه را در قسمت URL وارد کنید
5. در صورت نیاز، API Key را در قسمت مربوطه وارد کنید
6. روی `اتصال` کلیک کنید تا لیست لایه‌های موجود نمایش داده شود
7. لایه مورد نظر را انتخاب و به نقشه اضافه کنید

### استفاده از  API

برای توسعه‌دهندگان، می‌توان از درخواست‌های HTTP مستقیم استفاده کرد:

#### 1. عملیات GetCapabilities

این درخواست اطلاعات کلی درباره سرویس WFS و لایه‌های موجود را برمی‌گرداند:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.0&request=GetCapabilities'
```

پارامترها:

- `{your ip}`: آدرس سرور سامانه مورد نظر
- `{your apikey}`: کلید API دریافتی از کارشناس سامانه
- `service=wfs`: مشخص می‌کند که درخواست مربوط به سرویس WFS است
- `version=1.1.0`: نسخه پروتکل WFS مورد استفاده
- `request=GetCapabilities`: نوع عملیات درخواستی

#### 2. عملیات DescribeFeatureType

این درخواست ساختار داده‌ای یک لایه خاص را برمی‌گرداند:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=DescribeFeatureType&typeNames={layername}'
```

پارامترها:

- `typeNames={layername}`: نام لایه مورد نظر که می‌خواهید ساختار آن را دریافت کنید

> **نکته**: در نسخه‌های 1.1.1 و بالاتر، فیلتر نام لایه تأثیرگذار خواهد بود.

#### 3. عملیات GetFeature

##### 1. دریافت تمام داده‌ها (بدون فیلتر)

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames={layername}'
```

##### 2. فیلتر با شناسه عارضه (featureID)

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames=geotajak:{layername}&featureID={featureID}'
```

پارامترها:

- `featureID={featureID}`: شناسه منحصر به فرد عارضه مورد نظر

##### 3. محدود کردن تعداد نتایج

**در نسخه 1.1.0**:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.0&request=GetFeature&typeNames={layername}&maxFeatures={count}'
```

پارامترها:

- `maxFeatures={count}`: حداکثر تعداد عوارض برگشتی

**در نسخه 1.1.1 و بالاتر**:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1'
```

پارامترها:

- `count={count}`: تعداد عوارض درخواستی

##### 4. مرتب‌سازی نتایج براساس یک فیلد

**مرتب‌سازی صعودی**:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&sortBy={fieldname}'
```

پارامترها:

- `sortBy={fieldname}`: نام فیلد مورد نظر برای مرتب‌سازی (صعودی)

**مرتب‌سازی نزولی**:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&sortBy={fieldname}+D'
```

> **نکته**: برای مرتب‌سازی نزولی، کافی است `+D` را به انتهای نام فیلد اضافه کنید.

##### 5. انتخاب فیلدهای خاص در خروجی

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&propertyName={fieldname1},{fieldname2}'
```

پارامترها:

- `propertyName={fieldname1},{fieldname2}`: لیست فیلدهای مورد نیاز در خروجی (با کاما جداسازی می‌شوند)

##### 6. فیلتر با محدوده مکانی (BBox)

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&version=1.1.1&srsName={crs}:4326&bbox={bbox},{crs}'
```

پارامترها:

- `bbox={bbox}`: محدوده مختصاتی مورد نظر (معمولاً به صورت `minX,minY,maxX,maxY`)
- `{crs}`: سیستم مرجع مختصات مورد استفاده (مانند `EPSG:4326`)

## نکات تکمیلی

### فرمت‌های خروجی

WFS می‌تواند داده‌ها را در فرمت‌های مختلفی ارائه دهد. برای مشخص کردن فرمت خروجی، می‌توانید از پارامتر `outputFormat` استفاده کنید:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames={layername}&outputFormat=application/json'
```

فرمت‌های رایج شامل:

- `application/json` یا `json` برای GeoJSON
- `GML2` برای Geography Markup Language نسخه 2
- `GML3` برای Geography Markup Language نسخه 3
- `csv` برای خروجی مقادیر جدا شده با کاما
- `SHAPE-ZIP` برای فایل شیپ فشرده‌شده

### فیلترهای پیشرفته

WFS از زبان فیلترینگ قدرتمندی پشتیبانی می‌کند که امکان جستجوهای پیچیده را فراهم می‌سازد:

```bash
curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames={layername}&filter=<Filter><PropertyIsEqualTo><PropertyName>{fieldname}</PropertyName><Literal>{value}</Literal></PropertyIsEqualTo></Filter>'
```

این مثال عوارضی را برمی‌گرداند که مقدار فیلد مشخص شده با مقدار موردنظر برابر باشد.

### بهینه‌سازی عملکرد

برای بهبود عملکرد در کار با سرویس WFS، این نکات را رعایت کنید:

1. همیشه از پارامتر `count` یا `maxFeatures` برای محدود کردن تعداد نتایج استفاده کنید
2. فقط فیلدهای مورد نیاز را با `propertyName` درخواست کنید
3. در صورت امکان، از فیلترهای مکانی مانند `bbox` استفاده کنید
4. برای کاهش حجم داده‌های منتقل شده، از فرمت‌های فشرده مانند GeoJSON استفاده کنید