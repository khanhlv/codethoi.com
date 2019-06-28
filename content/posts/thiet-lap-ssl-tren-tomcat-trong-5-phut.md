+++
title = "Thiết lập SSL trên Tomcat trong 5 phút"
description = "Thiết lập SSL trên Tomcat trong 5 phút"
tags = ["SSL", "Tomcat"]
keywords = ["SSL", "Tomcat"]
date = "2019-06-28"
+++
Hướng dẫn bạn cách định cấu hình SSL (https://localhost:8443) trên Tomcat trong 5 phút.

Cần chuẩn bị:

* Java SDK
* Tomcat

Cấu hình gồm 3 bước cơ bản:

    1. Tạo **keystore** bằng Java
    2. Cấu hình **Tomcat** sử dụng *keystore*
    3. Kiểm thử
    4. (Tip) Cấu hình ứng dụng của bạn chạy SSL (https://localhost:8443/yourApp) 


# 1. Tạo **keystore** bằng Java

Mở terminal trên máy tính của bạn và gõ:

**Windows :**

```
cd %JAVA_HOME%/bin
```

**Linux or Mac OS:**

```
cd $JAVA_HOME/bin
```
Tip: JAVA_HOME của MAC */System/Library/Frameworks/JavaVM.framework/Versions/{your java version}/Home/*

Tiếp theo, gõ:

```
keytool -genkey -alias tomcat -keyache RSA -keystore /path/keystore
```

Khi bạn gõ lệnh trên, nó sẽ hỏi bạn một số câu hỏi. Đầu tiên, nó sẽ yêu cầu bạn tạo một mật khẩu

```
Enter keystore password:  password
Re-enter new password: password
What is your first and last name?
  [Unknown]:  Loiane Groner
What is the name of your organizational unit?
  [Unknown]:  home
What is the name of your organization?
  [Unknown]:  home
What is the name of your City or Locality?
  [Unknown]:  Sao Paulo
What is the name of your State or Province?
  [Unknown]:  SP
What is the two-letter country code for this unit?
  [Unknown]:  BR
Is CN=Loiane Groner, OU=home, O=home, L=Sao Paulo, ST=SP, C=BR correct?
  [no]:  yes
 
Enter key password for
    (RETURN if same as keystore password):  password
Re-enter new password: password

```

# 2. Cấu hình **Tomcat** sử dụng *keystore*

Mở thư mục cài đặt Tomcat của bạn và mở thư mục **conf** . Trong thư mục này, bạn sẽ tìm thấy tệp **server.xml** . Mở nó ra.

Tìm khai báo sau:
```
<!--
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
    maxThreads="150" scheme="https" secure="true"
    clientAuth="false" sslProtocol="TLS" />
-->
```

Bỏ comment và sửa:

```
<Connector SSLEnabled="true" acceptCount="100" clientAuth="false"
    disableUploadTimeout="true" enableLookups="false" maxThreads="25"
    port="8443" keystoreFile="/Users/loiane/keystore" keystorePass="password"
    protocol="org.apache.coyote.http11.Http11NioProtocol" scheme="https"
    secure="true" sslProtocol="TLS" />
```
# 3. Kiểm thử

Khở động Tomcat và truy cập đường dẫn https://localhost:8443

# 4. (Tip) Cấu hình ứng dụng của bạn chạy SSL (https://localhost:8443/yourApp) 

Để buộc ứng dụng web của bạn hoạt động với SSL, bạn chỉ cần thêm mã sau vào tệp **web.xml** trong Tomcat

```
<security-constraint>
    <web-resource-collection>
        <web-resource-name>ERP APPLICATION</web-resource-name>
        <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
        <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
</security-constraint>
```

Nếu bạn muốn tắt SSL, bạn không cần xóa mã ở trên khỏi **web.xml**, chỉ cần thay đổi CONFIDENTIAL thành KHÔNG .

# Tài liệu tham khảo
[http://tomcat.apache.org/tomcat-7.0-doc/ssl-howto.html](http://tomcat.apache.org/tomcat-7.0-doc/ssl-howto.html)

[https://dzone.com/articles/setting-ssl-tomcat-5-minutes](https://dzone.com/articles/setting-ssl-tomcat-5-minutes)

