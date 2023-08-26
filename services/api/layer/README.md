# layer API

در قدم اول از کارشنا سامانه خود بخواهید که دسترسی نمایش مستندات api سامانه را برای شما فعال کند

در ادامه به انتهای ادرس سامانه
/api/docs
اضافه کنید تا وارد صفحه داکیومنت api
شوید

بعد از وارد شدن به این آدرس با صفحه ای مانند تصویر زیر روبرو خواهید شد

![api docs sample page](https://github.com/SaaFaa-company/geotajak3-documents/blob/main/services/image/apidoc.png?raw=true "api docs sample page")

در این صفحه لیست تمام api های موجود در سامانه را مشاهده می کنیم

در این بخش آموزش به استفاده کردن از api های ارائه شده ماژول لایه ها می پردازیم


- دریافت لیست لایه ها
    - متد get
    - احراز هویت: barer token در هدر
    - آدرس: http://{your ip}/api/layers
        - {your ip}: آدرس سامانه مورد نظر
    
    - نمونه درخواست با curl
        - ```
          curl --location --request GET 'http://192.168.11.73/api/layers' --header 'Authorization: Bearer {your apikey}'
          ```
            - {your apikey} : کلید دسترسی که از کارشناس سامانه دریافت می کنید
    
- دریافت لیست فیلد های لایه
    - متد get
    - احراز هویت: barer token در هدر
    - آدرس: http://{your ip}/api/layers/{layer id}/attributes/
        - {your ip}: آدرس سامانه مورد نظر
        - {layer id}: آی دی لایه مورد نظر
    
    - نمونه درخواست با curl
        - ```
           curl --location --request GET 'http://{your ip}/api/layers/{layer id}/attributes/' --header 'Authorization: Bearer {your apikey}'
          ```
            - {your apikey} : کلید دسترسی که از کارشناس سامانه دریافت می کنید
            - {your ip}: آدرس سامانه مورد نظر
            - {layer id}: آی دی لایه مورد نظر 