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
      curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.0&request=GetCapabilities'
      ```
        - {your apikey} : کلید دسترسی که از کارشناس سامانه دریافت می کنید
  
  - عملیات DescribeFeatureType
    - ```
      curl --location --request GET 'http://192.168.11.73/api/proxy/api_key/{your apikey}/wfs/?service=wfs&version=1.1.1&request=DescribeFeatureType&typeNames={layername}'
      ```
        - {layername} : نام لایه
  
  
