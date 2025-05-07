
## پیش‌نیازها (Prerequisites)

برای استفاده از این API، شما نیاز به موارد زیر دارید:

- دسترسی به سامانه مورد نظر
- کلید API (API Key) که از کارشناس سامانه دریافت می‌کنید

## دسترسی به مستندات Swagger

برای مشاهده مستندات API در قالب Swagger، مراحل زیر را دنبال کنید:

1. از کارشناس سامانه بخواهید دسترسی نمایش مستندات API را برای شما فعال کند
2. به انتهای آدرس سامانه، عبارت `/api/docs` را اضافه کنید
3. پس از وارد شدن، صفحه‌ای مشابه تصویر زیر مشاهده خواهید کرد:

![api docs sample page](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/Images/apidoc.png?raw=true "api docs sample page")


## API‌های ماژول لایه‌ها (Layer Module APIs)

### 1. دریافت لیست لایه‌ها (Get Layers List)

این API برای دریافت لیست تمامی لایه‌های موجود در سامانه استفاده می‌شود.

**مشخصات درخواست:**

- **متد:** GET
- **احراز هویت:** Bearer Token در هدر
- **آدرس:** `http://{your_ip}/api/layers`
    - `{your_ip}`: آدرس سامانه مورد نظر شما

**نمونه درخواست با cURL:**

```bash
curl --location --request GET 'http://{your_ip}/api/layers' \
--header 'Authorization: Bearer {your_apikey}'
```

**پارامترها:**

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر

**نمونه پاسخ:**

```json
{
  "layers": [
    {
      "id": 1,
      "name": "layer_name_1",
      "description": "Layer description"
      // سایر اطلاعات مربوط به لایه
    },
    {
      "id": 2,
      "name": "layer_name_2",
      "description": "Layer description"
      // سایر اطلاعات مربوط به لایه
    }
    // ...
  ],
  "total": 10
}
```

### 2. دریافت لیست فیلدهای لایه (Get Layer Attributes)

این API برای دریافت تمامی فیلدها و ویژگی‌های یک لایه خاص استفاده می‌شود.
اگه اشتباه نکنم یه چیزی شبیه به متد OPTION تو ریکوئسته

**مشخصات درخواست:**

- **متد:** GET
- **احراز هویت:** Bearer Token در هدر
- **آدرس:** `http://{your_ip}/api/layers/{layer_id}/attributes/`
    - `{your_ip}`: آدرس سامانه مورد نظر
    - `{layer_id}`: شناسه لایه مورد نظر

**نمونه درخواست با cURL:**

```bash
curl --location --request GET 'http://{your_ip}/api/layers/{layer_id}/attributes/' \
--header 'Authorization: Bearer {your_apikey}'
```

**پارامترها:**

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر
- `{layer_id}`: شناسه لایه مورد نظر

**نمونه پاسخ:**

```json
{
  "attributes": [
    {
      "name": "attribute_name_1",
      "type": "string",
      "description": "Attribute description"
      // سایر اطلاعات مربوط به فیلد
    },
    {
      "name": "attribute_name_2",
      "type": "number",
      "description": "Attribute description"
      // سایر اطلاعات مربوط به فیلد
    }
    // ...
  ]
}
```

### 3. دریافت فیچرهای لایه (Get Layer Features)

این API برای دریافت فیچرهای (عوارض) موجود در یک لایه خاص استفاده می‌شود. شما می‌توانید تعداد خروجی را با استفاده از پارامترهای مختلف محدود کنید.

**مشخصات درخواست:**

- **متد:** GET
- **احراز هویت:** Bearer Token در هدر
- **آدرس:** `http://{your_ip}/api/layers/{layer_id}/features/?outputFormat=json&is_form=true&limit={limit}&offset={offset}&maxFeatures={max_feature}`
    - `{your_ip}`: آدرس سامانه مورد نظر
    - `{layer_id}`: شناسه لایه مورد نظر
    - `{limit}`: محدودیت تعداد خروجی (برای مثال: 100)
    - `{offset}`: نقطه شروع شمارش (برای مثال: 0 برای شروع از اولین رکورد)
    - `{max_feature}`: حداکثر تعداد فیچرهای خروجی

**نمونه درخواست با cURL:**

```bash
curl --location --request GET 'http://{your_ip}/api/layers/{layer_id}/features/?outputFormat=json&is_form=true&limit={limit}&offset={offset}&maxFeatures={max_feature}' \
--header 'Authorization: Bearer {your_apikey}'
```

**پارامترها:**

- `{your_apikey}`: کلید دسترسی که از کارشناس سامانه دریافت می‌کنید
- `{your_ip}`: آدرس سامانه مورد نظر
- `{layer_id}`: شناسه لایه مورد نظر
- `{limit}`: محدودیت تعداد خروجی (مثلاً 100)
- `{offset}`: نقطه شروع شمارش (مثلاً 0)
- `{max_feature}`: حداکثر تعداد فیچرهای خروجی

**پارامترهای اختیاری:**

- `outputFormat`: فرمت خروجی (json توصیه می‌شود)
- `is_form`: اگر true باشد، خروجی برای نمایش در فرم بهینه می‌شود

**نمونه پاسخ:**

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [51.123456, 35.123456]
      },
      "properties": {
        "name": "Feature name",
        "description": "Feature description",
        // سایر ویژگی‌های فیچر
      }
    }
    // ...
  ],
  "totalFeatures": 150,
  "numberMatched": 150,
  "numberReturned": 100
}
```

## نکات تکمیلی (Additional Notes)

- برای بهینه‌سازی عملکرد، از پارامترهای `limit` و `offset` برای صفحه‌بندی نتایج استفاده کنید.
- توجه داشته باشید که برای دریافت فیچرهای لایه‌های بزرگ، ممکن است زمان پاسخگویی طولانی شود.


## کدهای خطا (Error Codes)

در صورت بروز خطا، API پاسخی با کد وضعیت HTTP مناسب و پیام خطا برمی‌گرداند:

- `401`: احراز هویت ناموفق (API Key نامعتبر)
- `403`: عدم دسترسی به منبع درخواستی
- `404`: منبع درخواستی یافت نشد
- `500`: خطای داخلی سرور