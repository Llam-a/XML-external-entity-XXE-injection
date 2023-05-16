# Overview

Một số ứng dụng cho phép người dùng tải lên các tập tin được xử lý phía máy chủ. Một số định dạng tập tin phổ biến sử dụng XML hoặc chứa các thành phần con XML. Ví dụ về các định dạng dựa trên XML là định dạng tài liệu văn phòng như DOCX và định dạng hình ảnh như SVG.

Ví dụ, một ứng dụng có thể cho phép người dùng tải lên hình ảnh và xử lý hoặc xác thực chúng trên máy chủ sau khi tải lên. Ngay cả khi ứng dụng mong đợi nhận định dạng như PNG hoặc JPEG, thư viện xử lý hình ảnh đang được sử dụng có thể hỗ trợ hình ảnh SVG. Vì định dạng SVG sử dụng XML, một kẻ tấn công có thể gửi một hình ảnh SVG độc hại và tận dụng các lỗ hổng XXE ẩn trong đó.Ví dụ như:

```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```
