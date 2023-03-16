+++
title = "Hưỡng dẫn reset thời gian dùng thử Navicat Premium 15/16 Window"
description = "Navicat Premium là một phần mềm cực kì hữu ích, Navicat Premium có thể giúp bạn kết nối, đồng bộ, quản trị một cách đơn giản và dễ dàng đối với nhiều hệ cơ sở dữ liệu khác nhau như: MySQL, Oracle, PostgreSQL, MariaDB, SQLite, SQL Server."
tags = ["Navicat Premium", "Navicat", "reset trial Navicat Premium", "Navicat Premium 16 reset trial", "Navicat reset trial","Navicat Premium reset trial", "Navicat Premium 16", "Navicat Premium 15", "Navicat Premium 15/16", "reset thời gian dùng thử Navicat Premium"]
keywords = ["Navicat Premium", "Navicat", "reset trial Navicat Premium", "Navicat Premium 16 reset trial", "Navicat reset trial","Navicat Premium reset trial", "Navicat Premium 16", "Navicat Premium 15", "Navicat Premium 15/16", "reset thời gian dùng thử Navicat Premium"]
date = "2023-03-16"
+++

Navicat Premium là một phần mềm cực kì hữu ích, Navicat Premium có thể giúp bạn kết nối, đồng bộ, quản trị một cách đơn giản và dễ dàng đối với nhiều hệ cơ sở dữ liệu khác nhau như: MySQL, Oracle, PostgreSQL, MariaDB, SQLite, SQL Server...


![](https://www.navicat.com/images/product_screenshot/02.Product_01_Premium_Windows_01_Mainscreen15.png)

Nhà mình nghèo mà muốn dùng tool xịn, mà lương tâm không cắn rứt thì thôi đành dùng cách reset thời gian dùng thử để sử dụng tiếp.


## Delete Navicat Registry File

**HKEY_CURRENT_USER\Software\PremiumSoft\NavicatPremium\Registration[version and language]**

- ví dụ : Registration15XCT, Registration16XEN

**HKEY_CURRENT_USER\Software\Classes\CLSID\ * \Info**

- Delete all "Info" folder under CLSID (Parent folder name of Info may vary from person to person)
- Be sure that will not delete other important file

Code
```
@echo off

echo Delete HKEY_CURRENT_USER\Software\PremiumSoft\NavicatPremium\Registration[version and language]
for /f %%i in ('"REG QUERY "HKEY_CURRENT_USER\Software\PremiumSoft\NavicatPremium" /s | findstr /L Registration"') do (
    reg delete %%i /va /f
)
echo.

echo Delete Info folder under HKEY_CURRENT_USER\Software\Classes\CLSID
for /f %%i in ('"REG QUERY "HKEY_CURRENT_USER\Software\Classes\CLSID" /s | findstr /E Info"') do (
    reg delete %%i /va /f
)
echo.

echo Finish

pause
```

Có thể tải [*tại đây*](https://codethoi.com/navicat-refresh.bat)