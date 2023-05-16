# Overview

Một số ứng dụng nhận dữ liệu được gửi bởi khách hàng, nhúng nó vào tài liệu XML phía máy chủ và sau đó phân tích tài liệu đó. Một ví dụ về điều này xảy ra khi dữ liệu được gửi bởi khách hàng được đặt vào một yêu cầu SOAP phía sau, sau đó được xử lý bởi dịch vụ SOAP phía sau.

Trong tình huống này, bạn không thể thực hiện một cuộc tấn công XXE cổ điển, vì bạn không kiểm soát toàn bộ tài liệu XML và do đó không thể định nghĩa hoặc sửa đổi một phần tử DOCTYPE. Tuy nhiên, bạn có thể sử dụng XInclude thay vào đó. XInclude là một phần của thông số kỹ thuật XML cho phép xây dựng một tài liệu XML từ các tài liệu con. Bạn có thể đặt một cuộc tấn công XInclude trong bất kỳ giá trị dữ liệu nào trong tài liệu XML, vì vậy cuộc tấn công có thể được thực hiện trong những tình huống mà bạn chỉ kiểm soát một mục dữ liệu duy nhất được đặt vào tài liệu XML phía máy chủ.

Để thực hiện một cuộc tấn công XInclude, bạn cần tham chiếu tới không gian tên XInclude và cung cấp đường dẫn đến tập tin mà bạn muốn bao gồm.Ví dụ như:

```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```

Cuộc tấn công XInclude đề cập đến một lỗ hổng bảo mật khi kẻ tấn công tận dụng tính năng XInclude trong XML để bao gồm và thao tác nội dung từ bên ngoài vào tài liệu XML. Tính năng XInclude cho phép xây dựng các tài liệu XML từ các tài liệu con, cung cấp một cơ chế cho tính mô-đun và tái sử dụng.

Trong cuộc tấn công XInclude, kẻ tấn công thường tạo một tài liệu XML độc hại hoặc đầu vào được thiết kế để khai thác tính năng XInclude để bao gồm nội dung không được ủy quyền hoặc không mong đợi. Mục tiêu thường là lấy thông tin nhạy cảm hoặc thực thi mã tùy ý phía máy chủ.

Thực hành ở đây
