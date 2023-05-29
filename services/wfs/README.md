# سرویس WFS
در این بخش به توضیحات سرویس WFS می‌پردازیم.

### تعریف
سرویس WMS خلاصه شده‌ی Web Feature Service می‌باشد.

###### کاربرد های سرویس WMS

- دریافت داده های لایه
- ویرایش داده های لایه (افزودن، ویرایش و حذف)
- دریافت مشخصات لایه(فیلد های لایه و ...)

### عملیات های قابل پشتیبانی

![wfs supported operations](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/image/wfs-oprations.png?raw=true "wfs supported operations")

- عملیات GetCapabilities
    - فرا داده ای مربرط به سرویسی که سرور قابلیت ارائه دارد را ایجاد می‌کند همچنین عملیات و پارامتر های معتبر WFS را توصیف می‌کند
- عملیات DescribeFeatureType
    - اطلاعاتی درمورد فیلد های لایه باز می‌گرداند
- عملیات GetFeature
    - داده های لایه مورد نظر را باز می‌گرداند
- عملیات Transaction
    - برای عملیات روی داده های لایه
    
## استفاده از سرویس WFS سامانه ژئوتاژک
توجه داشته باشیدقبل از استفاده از مثال های این بخش باید از کارشناس سامانه درخواست Apikey و آدرس سرویس WFS را بدهید.

- استفاده در نرم‌افزار QGIS
  - ![add wfs to qgis](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/image/add-wfs-qgis.png?raw=true "add wfs to qgis")
    - مطابق تصویر بالا آدرس WFS را در قسمت url قرار می‌دهیم و از سرویس مورد نظر استفاده می‌کنیم
  
- با استفاده از request
  - عملیات GetCapabilities
    - ```
      curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.0&request=GetCapabilities'
      ```
        - {your apikey} : کلید دسترسی که از کارشناس سامانه دریافت می کنید
        - {your ip} : آدرس سامانه مورد نظر
  
  - عملیات DescribeFeatureType
    - ```
      curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=DescribeFeatureType&typeNames={layername}'
      ```
        - {layername} : نام لایه
        - توجه داشته باشید در ورژن های 1.1.1 و بعد از آن فیلتر نام لایه تاثیر گذار خواهد بود
  
  - عملیات GetFeature
    - تمام داده ها (بدون فیلتر)
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames={layername}'
        ```
    
    - فیلتر با featureID
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=GetFeature&typeNames=geotajak:{layername}&featureID={featureID}'
        ```
        - {featureID} : ای‌دی فیچر مورد نظر
  
    - فیلتر تعداد
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.0&request=GetFeature&typeNames={layername}&maxFeatures={count}'
        ```
        - {count} : تعداد مورد نظر
        - توجه داشته باشید فیلتر تعداد (maxFeatures) تنها در ورژن 1.1.0 استفاده می‌شود
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1'
        ```
        - توجه داشته باشید فیلتر تعداد (count) تنها در ورژن های 1.1.1 به بعد قابل استفاده است
    
    - فیلتر با کمک ترتیب یک فیلد
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&sortBy={fieldname}'
        ```
        - {fieldname} : نام فیلد مورد نظر موجود در لایه

    - فیلتر برعکس با کمک ترتیب یک فیلد
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&sortBy={fieldname}+D'
        ```
        - برای فیلتر به صورت برعکس تنها کافی است +D به اخر نام فیلد اضافه کنید
    
    - فیلتر فیلد ها در خروجی
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&count={count}&version=1.1.1&propertyName={fieldname1},{fieldname2}'
        ```
        - {propertyName} : نام فیلد های مورد نیاز در خروجی (با کاما جدا شود)
  
    - فیلتر با کمک محدوده نمایش (bbox)
      - ```
        curl --location --request GET 'http://{your ip}/api/proxy/api_key/{your apikey}/wfs/?service=wfs&request=GetFeature&typeNames={layername}&version=1.1.1&srsName={crs}:4326&bbox={bbox},{crs}'
        ```
        - {bbox} : محدوده نمایش مورد نظر
        - {crs} : نام پروژکشن مورد نظر مانند EPSG:4326