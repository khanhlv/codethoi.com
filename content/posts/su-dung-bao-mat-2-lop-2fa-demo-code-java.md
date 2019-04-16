+++
title = "Sử dụng bảo mật 2 lớp (2FA), demo bằng ngôn ngữ Java"
description = "Sử dụng bảo mật 2 lớp (2FA), demo bằng ngôn ngữ Java"
tags = ["2FA"]
keywords = ["2FA","bảo mật 2 lớp","bảo mật 2"]
date = "2019-04-09"
+++
Bài hôm trước mình có giới thiệu về bảo mật 2 lớp (2FA), hôm nay mình tiếp làm demo cơ bản về 2FA và sử dụng nó bằng ngôn ngữ Java

Như hôm trước để xác thực 2 lớp cần có

* 1 khóa bí mật chia sẻ (shared secret - một dãy các byte).
* 1 đầu vào là thời gian hiện tại.
* 1 hàm mã hóa.

# Các bước thực thiện
    1. Thư viện common-codec
    2. Khóa bí mật
    3. Mã hóa 
    4. Chạy thử
# Thư viện common-codec
Mình có dùng thư viện commons-codec, các bạn mở file pom.xml
```
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.6</version>
</dependency>
```
# Khóa bí mật
Khóa bí mật này tùy từng hệ thống có các tạo khóa bí mật khác nhau, 16, 32, 64, 128 ... ký tự

Như mình sẽ sử dụng 32 ký tự. Các bạn có thể dùng sẵn 1 số lib của commons-codec

```
public static String generateBase32Secret(int length) {
    StringBuilder sb = new StringBuilder(length);
    Random random = new SecureRandom();
    for (int i = 0; i < length; i++) {
        int val = random.nextInt(32);
        if (val < 26) {
            sb.append((char) ('A' + val));
        } else {
            sb.append((char) ('2' + (val - 26)));
        }
    }
    return sb.toString();
}
```
Hàm này mình truyền vào độ dài của khóa ký tự, bạn muốn là bao nhiêu sẽ là bấy nhiêu

Kết quả sẽ như thế này: ``YJC5DTNL27744YLACGZFW5HY2AOUUE6F``

Tạo QR Code
```
https://chart.googleapis.com/chart?chs=200x200&cht=qr&chl=200x200&chld=M|0&cht=qr&chl=otpauth://totp/khanhlv.group@gmail.com%3Fsecret%3DYJC5DTNL27744YLACGZFW5HY2AOUUE6F%26issuer%3DGoogleTest
```

# Mã hóa
Khi có khóa rồi mình làm bước tiếp theo mã hõa

***hmac = SHA1(secret + SHA1(secret + input))***

```
public static long generateNumber(String base32Secret, long timeMillis, long timeStepSeconds)
        throws GeneralSecurityException {
    byte[] key = new Base32().decode(base32Secret);

    byte[] data = new byte[8];
    long value = timeMillis / 1000 / timeStepSeconds;
    for (int i = 7; value > 0; i--) {
        data[i] = (byte) (value & 0xFF);
        value >>= 8;
    }

    SecretKeySpec signKey = new SecretKeySpec(key, "HmacSHA1");
    Mac mac = Mac.getInstance("HmacSHA1");
    mac.init(signKey);
    byte[] hash = mac.doFinal(data);

    // take the 4 least significant bits from the encrypted string as an offset
    int offset = hash[hash.length - 1] & 0xF;

    // We're using a long because Java hasn't got unsigned int.
    long truncatedHash = 0;
    for (int i = offset; i < offset + 4; ++i) {
        truncatedHash <<= 8;
        // get the 4 bytes at the offset
        truncatedHash |= (hash[i] & 0xFF);
    }
    // cut off the top bit
    truncatedHash &= 0x7FFFFFFF;

    // the token is then the last 6 digits in the number
    truncatedHash %= 1000000;

    return truncatedHash;
}
```

``
String base32Secret là khóa bí mật
long timeMillis là thời gian hiện tại của hệ thống
long timeStepSeconds là thời gian hết hạn, mặt định là 30s
``
# Chạy thử
```
public static void main(String[] args) throws Exception {
    long DEFAULT_TIME_STEP_SECONDS = 30;
    String base32Secret = "YJC5DTNL27744YLACGZFW5HY2AOUUE6F";

    System.out.println(new String(decodeBase32(base32Secret)));
    System.out.println("Secret = " + base32Secret);

    String keyId = "khanhlv.group@gmail.com";
    Long code = null;

    while (true) {
        long diff = DEFAULT_TIME_STEP_SECONDS - ((System.currentTimeMillis() / 1000) % DEFAULT_TIME_STEP_SECONDS);
        code = generateNumber(base32Secret, System.currentTimeMillis(), DEFAULT_TIME_STEP_SECONDS);
        System.out.println("Secret code = " + code + ", change in " + diff + " seconds");
        Thread.sleep(1000);
    }
}
```
Kết quả:

```
Secret = YJC5DTNL27744YLACGZFW5HY2AOUUE6F
Secret code = 706313, change in 26 seconds
Secret code = 706313, change in 25 seconds
Secret code = 706313, change in 24 seconds
Secret code = 706313, change in 23 seconds
Secret code = 706313, change in 22 seconds
```
Bây giờ các bạn có thể dùng áp dụng 2 lớp cho hệ thống mình rồi.

Và có thể thay thế Google Authenticator rồi, đỡ phải cài đặt ứng dụng =)))

# Kết luận
2FA là một kĩ thuật dùng để enhance security layer của một application. Hay nói cách khác, bạn khóa 1 cửa bằng 2 cái khóa luôn an toàn hơn 1 cái.

# Bài liên quan
[*Bảo mật 2 lớp (2FA) là gì ? Google Authenticator hoạt động như thế nào ?*](https://codethoi.com/posts/bao-mat-2-lop-2fa-la-gi-google-authenticator-hoat-dong-nhu-the-nao/)
