"Stacking entities" (cũng được gọi là "recursive entities") là một kỹ thuật trong XML External Entity (XXE) attacks, trong đó các enity XML được chồng lên nhau để tạo ra sự mở rộng đệ quy và tạo ra các tác động không mong muốn.

Trong XXE, các entity XML cho phép định nghĩa các chuỗi văn bản và tái sử dụng chúng trong tài liệu XML. Khi một entity được định nghĩa, nó có thể được tham chiếu và mở rộng trong nội dung của tài liệu XML.

Trong kỹ thuật stacking entities, các entity được khai báo và tham chiếu đệ quy. Điều này có nghĩa là một entity có thể chứa một entity khác và entity được chứa có thể chứa một entity khác nữa. Quá trình này tiếp tục cho đến khi đạt đến một độ sâu nhất định hoặc xảy ra lỗi.

Khi sử dụng stacking entities trong XXE attacks, kẻ tấn công tạo ra một chuỗi các entity được chồng lên nhau để tạo ra một lần mở rộng đệ quy và lấy trộm dữ liệu hoặc thực hiện các tác động không mong muốn.

Ví dụ:

```xml
<!DOCTYPE data [
    <!ENTITY % firstEntity "<!ENTITY % secondEntity SYSTEM 'file:///etc/passwd'>">
    %firstEntity;
]>
<data>&secondEntity;</data>
```

Trong ví dụ này, chúng ta định nghĩa hai entity (`firstEntity` và `secondEntity`). Entity `firstEntity` chứa một định nghĩa entity `secondEntity` tham chiếu tới tệp `/etc/passwd`. Khi entity `secondEntity` được gọi, nó sẽ mở rộng đến nội dung của `/etc/passwd` và chèn nó vào trong tài liệu XML.

