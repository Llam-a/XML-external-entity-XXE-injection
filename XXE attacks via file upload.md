# Tấn công XXE thông qua file upload

Một phương pháp khác để tấn công XXE là thông qua việc upload file. Khi ứng dụng cho phép người dùng tải lên các tệp XML và sau đó xử lý chúng, việc tải lên tệp có thể tạo ra các điểm yếu XXE.

Để thực hiện tấn công XXE thông qua tải lên tệp, bạn cần tạo một tệp XML chứa các thực thể bên ngoài và sử dụng đường dẫn đến tệp trên máy chủ để khai thác. Dưới đây là một ví dụ về cách thực hiện tấn công XXE thông qua tải lên tệp:

1. Tạo một tệp XML chứa các thực thể bên ngoài và đường dẫn đến tệp trên máy chủ:

```xml
<!DOCTYPE data [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<data>&xxe;</data>
```

2. Upload file XML chứa payload XXE lên ứng dụng.

3. Khi ứng dụng xử lý tệp XML tải lên, nó sẽ giải tham chiếu đến thực thể `xxe` và đọc nội dung của tệp `/etc/passwd`. Kết quả sẽ được trả về cho bạn.

Một số ứng dụng cho phép người dùng tải lên tệp tin được xử lý phía máy chủ. Một số định dạng tập tin phổ biến sử dụng XML hoặc chứa các thành phần con XML. Ví dụ về các định dạng dựa trên XML là các định dạng tài liệu văn phòng như DOCX và định dạng hình ảnh như SVG.

Ví dụ, một ứng dụng có thể cho phép người dùng tải lên hình ảnh và xử lý hoặc xác nhận chúng trên máy chủ sau khi chúng được tải lên. Ngay cả khi ứng dụng mong đợi nhận định dạng như PNG hoặc JPEG, thư viện xử lý hình ảnh đang được sử dụng có thể hỗ trợ các hình ảnh SVG. Vì định dạng SVG sử dụng XML, một kẻ tấn công có thể gửi một hình ảnh SVG độc hại và vượt qua các điểm yếu XXE ẩn.

Thực hành [ở đây](https://github.com/Llam-a/XML-external-entity-XXE-injection/blob/main/Exercises/Lab%3A%20Exploiting%20XXE%20via%20image%20file%20upload.md).
