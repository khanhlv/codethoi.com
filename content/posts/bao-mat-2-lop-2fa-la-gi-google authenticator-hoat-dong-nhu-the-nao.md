+++
title = "Bảo mật 2 lớp (2FA) là gì ? Google Authenticator hoạt động như thế nào ?"
description = "Bảo mật 2 lớp (2FA) là gì ? Google Authenticator hoạt động như thế nào ?"
tags = ["2FA","bảo mật 2 lớp","bảo mật 2"]
keywords = ["2FA","bảo mật 2 lớp","bảo mật 2"]
date = "2019-04-08"
+++
Khi rảnh chém gió trong Group AE Thiện Lành, có người anh em thiện lành có hỏi ai đã dùng 2FA chưa, và cách hoạt động và sử dụng thế nào ?

Rõ ràng mình đã thấy 2FA đã sử dụng ở rất nhiều website trên các sàn Bittrex, Binance, Gmail, hay rất nhiều ứng dụng khác.

Vậy là mình tìm hiểu 2FA là gì, hoạt động thế nào, áp dụng trong dự án thế nào ?

# Bảo mật 2 lớp (2FA) là gì?

Two-Factor Authentication (2FA) hay còn gọi là bảo mật 2 lớp, là một phương thức để chứng thực user bằng việc combine 2 factors khác nhau từ bộ source:

* Một cái gì đó bạn biết.
* Một cái gì đó bạn có.
* Một cái gì đó mà nó mặc nhiên như vậy.

Một ví dụ khá cơ bản của 2FA đó là khi bạn rút tiền ở ATM, bạn cần 2 thứ, một là cái thẻ (bạn có) và mã PIN (bạn biết) mới có khả năng thực hiện rút tiền.

![Two-Factor Authentication (2FA) là gì](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/7gklibkwls_image.png)

Như vậy nó áp dụng trong online authentication như thế nào?

Với bảo mật thông thường, bạn chỉ cần nhập username và password để đăng nhập tài khoản của mình, thứ bảo vệ duy nhất của bạn là mật khẩu. Đây là cái mà “bạn biết”. 2FA sẽ thêm một extra layer để bạn cần cung cấp cái mà “bạn có” nữa.

# Các loại 2FA

* Hardware Token
* SMS/Voice Based
* Software Token
* Push Notification
* Các loại khác

Như bạn thấy, có rất nhiều cách để mô phỏng cái mà “bạn có”.

Chẳng hạn, SMS là một sự lựa chọn không tồi, server gửi SMS về cho user để đăng nhập. Nhưng SMS lại ko quá an toàn (có thể bị intercepted), và bị vấn đề về network, việc delay có thể làm ảnh hưởng tới authentication process.

Vì nhiều lí do khác nhau nên team quyết định chọn dùng Software Token cho 2FA. Và từ bây giờ trong bài viết mình 2FA cũng được ám chỉ tới phương pháp sử dụng cryptographically key của Software Token.

# Cơ chế hoạt động bên trong của 2FA

Khi bạn enable 2FA cho tài khoản của mình, bạn sẽ nhận được một secret key based 32. Tùy vào mức độ security, độ dài của secret key có thể là 80, 128 hoặc 160 bit.

Các authenticator application sẽ scan secret này dưới dạng QR code (hoặc manually) và dùng nó để generate ra một HMAC-SHA1. Chuỗi HMAC này có thể là một trong 2 dạng:

* [Time-Based One-Time Password (TOTP)](https://en.wikipedia.org/wiki/Time-based_One-time_Password_algorithm)
* [HMAC-Based One-Time Password (HOTP)](https://en.wikipedia.org/wiki/HMAC-based_One-time_Password_algorithm)

Sau đó HMAC này sẽ được extracted và lấy ra 1 số int 4 byte, đó chính là code.

Một mã code sẽ valid trong 30 giây. Tuy nhiên không phải ai cũng có clock synced giống nhau, vì network latency các kiểu nên thường mọi người hay cho phép ở phạm vi cộng trừ 1 code, tức là 1 code sẽ valid trong 1 phút 30 giây. Điều này có thể giảm tính an toàn, nhưng lại tăng sự trải nghiệm đáng kể.

**Có rất nhiều ứng dụng cung cấp cho chúng ta xác thực 2FA, như Google, Microsoft hoặc Authy, giờ chúng ta thử xem Google hoạt động thế nào nhe ^_^**

## Google Authenticator hoạt động như thế nào ?

Google Authenticator là ứng dụng hiện thực hóa thuật toán Time-Based One-Time Password (TOTP). Nó bao gồm các thành phần sau:

* 1 khóa bí mật chia sẻ (shared secret - một dãy các byte).
* 1 đầu vào là thời gian hiện tại.
* 1 hàm mã hóa.

## Shared Secret
Trước hết cần sử dụng một khóa bí mật để thiết lập tài khoản trên điện thoại. Ta có thể chụp ảnh mã QR bằng điện thoại của mình hoặc có thể nhập theo cách thủ công. Trong trường hợp nhập thủ công, khóa bí mật của dịch vụ này được hiển thị theo định dạng sau:

```
xxxx xxxx xxxx xxxx xxxx
```
Mã QR chứa token tương tự là 1 URL:
```
otpauth://totp/Google%3Ayourname@gmail.com?secret=xxxx&issuer=Google
```
## Input (Current time)
Giá trị input đơn giản là thời giạn hiện tại của điện thoại của bạn, không cần có sự tương tác giữa client và server một khi đã có khóa bí mật. Tuy nhiên điều quan trọng là thời gian trên điện thoại phải trùng với thời gian trên server bởi server sẽ lặp lại chính xác những gì xảy ra tương tự trên điện thoại với input là thời gian hiện tại trên server.

Cụ thể hơn, server sẽ so sánh giá trị token mà người dùng submit với tất cả các token được sinh ra trong một khoảng thời gian nhất định (vài chục giây đến vài phút), nếu trùng nhau thì token bạn nhập là hợp lệ và pass qua vòng authentication thứ 2.

## Signing Function
Hàm mã hóa được sử dụng ở đây là **HMAC-SHA1**. HMAC là viết tắt của Hash-based message authentication code và nó là một thuật toán sử dụng hàm mã hóa một chiều (trong trường hợp này là SHA1) để mã hóa giá trị.

Sử dụng HMAC khá là an toàn bởi chỉ khi có khóa bí mật mới sinh được cùng một giá trị output cho cùng một giá trị input. 

Nghe thì phức tạp nhưng thuật toán thực tế thì đơn giản: ***hmac = SHA1(secret + SHA1(secret + input))***

## Algorithm
Trước hết ta cần base32 decode khóa bí mật. Vì Google hiển thị khóa bí mật bao gồm cả dấu cách và bằng chữ in thường để dễ đọc, nên ta cần loại bỏ dấu cách và uppercase chúng lên:
```
original_secret = xxxx xxxx xxxx xxxx xxxx xxxx xxxx xxxx
secret = BASE32_DECODE(TO_UPPERCASE(REMOVE_SPACES(original_secret)))
```
Tiếp theo lấy input là thời gian hiện tại của hệ thống:
```
input = CURRENT_UNIX_TIME()
```
Một điều dễ nhận thấy ở Google Authenticator là mã sinh ra thường hợp lệ trong 1 khoảng thời gian nhất định trước khi lại sinh ra một giá trị mới. Nếu giá trị này thay đổi liên tục mỗi giây thì rất khó cho người dùng kịp đọc hay copy paste nó. Giá trị mặc định là 30s, lấy thời gian hiện tại chia cho 30 thì trong 30s giá trị input là như nhau:
```
input = CURRENT_UNIX_TIME() / 30
```
Cuối cùng áp dụng hàm mã hóa HMAC-SHA1:
```
original_secret = xxxx xxxx xxxx xxxx xxxx xxxx xxxx xxxx
secret = BASE32_DECODE(TO_UPPERCASE(REMOVE_SPACES(original_secret)))
input = CURRENT_UNIX_TIME() / 30
hmac = SHA1(secret + SHA1(secret + input))
```
Cho đến thời điểm bây giờ, ta đã phần lớn hoàn thành dịch vụ xác thực 2 bước 2FA. Tuy nhiên kết quả ta thu được giá trị HMAC có độ dài tiêu chuẩn của một giá trị sau khi đi qua hàm mã hóa SHA1 (20 bytes, 40 ký tự hexa) và chắc chả ai muốn sử dụng dịch vụ này khi phải nhập 40 ký tự cả. Khoảng 6 kí tự là vừa đẹp.
```
four_bytes = hmac[LAST_BYTE(hmac):LAST_BYTE(hmac) + 4]
```
Ta có thể chuyển về dạng unsigned integer 32bit (4 bytes)

# Kết luận
2FA là một kĩ thuật dùng để enhance security layer của một application. Hay nói cách khác, bạn khóa 1 cửa bằng 2 cái khóa luôn an toàn hơn 1 cái. Trong xã hội đầy loạn lạc này thì ứng dụng nào quan trọng, chứa nhiều sensitive data và liên quan tới tiền bạc thì cứ auto bật 2FA thôi.

# Bài liên quan
[*Sử dụng bảo mật 2 lớp và code demo*](/posts/su-dung-bao-mat-2-lop-2fa-demo-code-java/)

# Tài liệu tham khảo
[https://garbagecollected.org/2014/09/14/how-google-authenticator-works/](https://garbagecollected.org/2014/09/14/how-google-authenticator-works/)

[http://runikitkat.com/post/2fa/](http://runikitkat.com/post/2fa/)

