+++
title = "Các thuật toán cân bằng tải phổ biến"
description = "Mô tả cách thức hoạt động của các thuật toán cân bằng tải phổ biến"
tags = ["load balancing algorithms", "balancing", "algorithms", "cân bằng tải"
, "load balancing", "balancing algorithms", "thuật toán tải", "thuật toán"]
keywords = ["load balancing algorithms", "balancing", "algorithms", "cân bằng tải"
, "load balancing", "balancing algorithms", "thuật toán tải", "thuật toán"]
date = "2023-02-17"
+++

Sơ đồ dưới đây cho thấy 6 thuật toán phổ biến.

![load balancing algorithms](/images/25122020/2020122501.PNG)


## Static Algorithms

1. Round robin

Các yêu cầu của máy khách được gửi đến các phiên bản dịch vụ khác nhau theo thứ tự tuần tự. Các dịch vụ thường được yêu cầu là không trạng thái.

2. Sticky round-robin

Đây là một cải tiến của thuật toán quay vòng. Nếu yêu cầu đầu tiên của Alice đến dịch vụ A, thì các yêu cầu sau cũng sẽ đến dịch vụ A.

3. Weighted round-robin

Quản trị viên có thể chỉ định trọng số cho từng dịch vụ. Những cái có trọng số cao hơn xử lý nhiều yêu cầu hơn những cái khác.

4. Hash

Thuật toán này áp dụng Hash trên IP hoặc URL của yêu cầu đến. Các yêu cầu được định tuyến đến các phiên bản có liên quan dựa trên kết quả của Hash.

## Dynamic Algorithms

5. Least connections

Một yêu cầu mới được gửi đến phiên bản dịch vụ có ít kết nối đồng thời nhất.

6. Least response time

Một yêu cầu mới được gửi đến phiên bản dịch vụ với thời gian phản hồi nhanh nhất.

Cơ bản là thế, nếu bạn muốn tìm hiểu kỹ hơn thì có thể nhờ anh Google nhe :)
