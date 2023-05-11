# XML-external-entity-XXE-injection

## Overview:

### XML là gì:

XML (Extensible Markup Language) là một ngôn ngữ đánh dấu dựa trên văn bản được sử dụng để lưu trữ và truyền dữ liệu có cấu trúc. Nó là một công nghệ chung cho việc trao đổi dữ liệu giữa các hệ thống khác nhau và được sử dụng rộng rãi trong ứng dụng web.

XML sử dụng các thẻ đánh dấu để xác định cấu trúc và nội dung của dữ liệu. Mỗi thẻ bắt đầu bằng một ký tự "<" và kết thúc bằng ký tự ">". Thẻ có thể chứa văn bản hoặc các thẻ con bên trong nó. Dữ liệu trong XML được tổ chức thành cây phân cấp, trong đó các thẻ cha chứa các thẻ con và các thẻ con có thể chứa các thẻ khác.

```
<person>
  <name>John Doe</name>
  <age>30</age>
  <email>john@example.com</email>
</person>
```

Trong ví dụ trên, chúng ta có một phần tử <person> chứa ba phần tử con là <name>, <age>, và <email>. Mỗi phần tử con chứa dữ liệu tương ứng, chẳng hạn <name> chứa "John Doe", <age> chứa "30", và <email> chứa "john@example.com".

XML cho phép người dùng tự định nghĩa các thẻ và cấu trúc dữ liệu phù hợp với nhu cầu của họ. Điều này giúp việc truyền và lưu trữ dữ liệu linh hoạt hơn và dễ dàng cho việc tương tác giữa các hệ thống khác nhau.

### External Entity (thực thể ngoại vi) là gì:

Trong ngữ cảnh của XML là một cơ chế cho phép tham chiếu và sử dụng dữ liệu từ các nguồn bên ngoài tài liệu XML hiện tại. Thực thể ngoại vi cho phép chèn dữ liệu từ các tệp tin, URL hoặc tài nguyên mạng vào trong tài liệu XML.

Trong XML, một thực thể ngoại vi được khai báo trong phần DTD (Document Type Definition) hoặc trong khai báo ENTITY. Nó có thể được định nghĩa bằng cách sử dụng một SYSTEM identifier (định danh hệ thống) để tham chiếu đến một nguồn bên ngoài.

Ví dụ về khai báo một thực thể ngoại vi trong DTD:
  
```
  <!DOCTYPE data [
  <!ENTITY externalEntity SYSTEM "http://example.com/data.xml">
]>
```
Trong ví dụ trên, externalEntity là tên của thực thể ngoại vi và http://example.com/data.xml là định danh hệ thống. Thực thể ngoại vi này tham chiếu đến tài liệu XML tại URL http://example.com/data.xml.

Thực thể ngoại vi trong XML có thể được sử dụng để chèn dữ liệu từ các nguồn bên ngoài vào tài liệu XML, nhưng cũng có thể gây ra các rủi ro bảo mật nếu không được xử lý đúng cách, như trong trường hợp của lỗ hổng XML External Entity (XXE) Injection.

### XXE là gì:
 
XXE là viết tắt của External Entity Expansion (mở rộng thực thể ngoại vi). Nó là một lỗ hổng bảo mật phổ biến trong các ứng dụng web, đặc biệt là trong các ứng dụng sử dụng XML để truyền và lưu trữ dữ liệu.

Khi một ứng dụng web không xử lý đầu vào XML đúng cách, tấn công XXE có thể cho phép kẻ tấn công chèn các thực thể ngoại vi (external entities) độc hại vào các tệp XML được sử dụng trong ứng dụng. Nhờ đó, kẻ tấn công có thể đọc các tệp hệ thống từ xa, thực hiện các cuộc tấn công phối hợp (coordinated attacks), và thậm chí thực hiện tấn công từ chối dịch vụ (DoS) bằng cách tăng cường đáng kể khối lượng công việc.

Các ứng dụng web cần kiểm tra và xử lý đầu vào XML một cách an toàn để ngăn chặn tấn công XXE. Cách phổ biến để ngăn chặn XXE là tắt tính năng mở rộng thực thể ngoại vi trong xử lý XML hoặc sử dụng bộ phân tích XML an toàn để đảm bảo chỉ các thực thể hợp lệ được xử lý.

## Nguyên do:
  
Lỗ hổng XXE (XML External Entity) phát sinh khi ứng dụng không xử lý đầu vào XML một cách an toàn. Dưới đây là một số nguyên nhân phổ biến dẫn đến sự tồn tại của lỗ hổng XXE:

- Không kiểm tra và xác thực đầu vào: Khi ứng dụng không thực hiện việc kiểm tra và xác thực đầu vào XML, các thực thể ngoại vi độc hại có thể được chèn vào tài liệu XML và được xử lý một cách không an toàn.

- Cho phép khai thác tính năng thực thể ngoại vi: Các ứng dụng một số ngôn ngữ hoặc thư viện XML cho phép mở rộng thực thể ngoại vi mặc định. Nếu tính năng này không được tắt hoặc kiểm soát cẩn thận, nó có thể tạo điều kiện cho việc khai thác lỗ hổng XXE.

- Tin cậy đối với dữ liệu không đáng tin cậy: Khi ứng dụng tin tưởng và xử lý dữ liệu XML từ nguồn không đáng tin cậy như người dùng hoặc bên thứ ba mà không kiểm tra tính toàn vẹn và đáng tin cậy của dữ liệu, lỗ hổng XXE có thể được khai thác.

- Sự phụ thuộc vào hàm xử lý XML không an toàn: Sử dụng các hàm xử lý XML không an toàn hoặc không được cập nhật có thể tạo điều kiện cho khai thác lỗ hổng XXE.

Để ngăn chặn lỗ hổng XXE, ứng dụng cần thực hiện các biện pháp bảo mật như kiểm tra và xác thực đầu vào, tắt tính năng mở rộng thực thể ngoại vi, sử dụng các bộ phân tích XML an toàn và giới hạn quyền truy cập đến các tài nguyên ngoại vi.
  
## Các loại tấn công XXE:
  
  Có 2 loại tấn công phổ biến:
  
  - Exploiting External Entity Declaration (In-band XXE)
  
  - Exploiting Parameter Entities (Out-of-band XXE)
  
  Ngoài ra còn có:
  
  - Exploiting XXE to retrieve files, trong đó một thực thể ngoại vi được định nghĩa chứa nội dung của một tệp tin, và được trả về trong phản hồi của ứng dụng.
  
  - Exploiting blind XXE to retrieve data via error messages, trong đó kẻ tấn công có thể kích hoạt một thông báo lỗi phân tích chứa dữ liệu nhạy cảm.
  
## Làm thế nào để tìm và kiểm tra các lỗ hổng XXE (XML External Entity) vulnerabilities?

Để tìm và kiểm tra các lỗ hổng XXE, bạn có thể tuân theo các bước sau:

- Xem xét các điểm tiếp xúc với dữ liệu XML: Tìm hiểu các thành phần trong ứng dụng của bạn mà có thể tiếp nhận hoặc xử lý dữ liệu XML, chẳng hạn như các giao diện API, form đăng ký, tải lên tệp tin XML, hoặc cơ sở dữ liệu lưu trữ XML.

- Kiểm tra DTD (Document Type Definition): DTD được sử dụng để định nghĩa cấu trúc của tài liệu XML. Tìm hiểu xem ứng dụng của bạn có chấp nhận hoặc xử lý DTD từ nguồn không đáng tin cậy không. Nếu ứng dụng cho phép khai báo ENTITY trong DTD, điều này có thể dẫn đến lỗ hổng XXE.

 - Kiểm tra xem liệu ứng dụng có chấp nhận dữ liệu XML từ nguồn bên ngoài: Xác định liệu ứng dụng có chấp nhận hoặc xử lý XML từ nguồn không đáng tin cậy không. Nếu ứng dụng đọc và xử lý XML từ nguồn bên ngoài, điều này có thể tạo ra lỗ hổng XXE.

- Kiểm tra xem liệu ứng dụng có phản hồi với thông báo lỗi XML: Gửi các dữ liệu XML độc hại hoặc chứa thực thể ngoại vi đến ứng dụng và quan sát phản hồi của nó. Nếu ứng dụng trả về thông báo lỗi XML chứa thông tin nhạy cảm, điều này có thể chỉ ra sự tồn tại của lỗ hổng XXE.

- Kiểm tra các kịch bản khai thác XXE: Thử áp dụng các kịch bản khai thác XXE vào ứng dụng để xem liệu chúng có thành công hay không. Điều này bao gồm chèn thực thể ngoại vi, đọc các tệp tin từ xa, thực hiện các yêu cầu mạng, hoặc tấn công SSRF.

- Sử dụng công cụ kiểm tra tự động: Có nhiều công cụ kiểm tra tự động có sẵn để tìm và kiểm tra các lỗ hổng XXE. Các công cụ này có thể giúp tự động tìm kiếm, phân tích và kiểm tra các lỗ hổng XX

## Cách phòng ngừa các lỗ hổng XXE (XML External Entity) vulnerabilities:

Để phòng ngừa các lỗ hổng XXE, bạn có thể thực hiện các biện pháp bảo mật sau đây:

1. Sử dụng cơ chế xử lý XML an toàn: Sử dụng các thư viện và công cụ xử lý XML an toàn và tuân thủ các hướng dẫn và tiêu chuẩn bảo mật khi xử lý dữ liệu XML trong ứng dụng của bạn. Đảm bảo rằng các cơ chế này loại bỏ hoặc vô hiệu hóa khả năng đọc và xử lý DTD (Document Type Definition) hoặc thực thể ngoại vi.

2. Tắt tính năng DTD và thực thể ngoại vi: Trong quá trình xử lý XML, hãy đảm bảo rằng các tính năng DTD và thực thể ngoại vi đã được tắt hoặc vô hiệu hóa. Điều này có thể được thực hiện bằng cách cấu hình thư viện XML hoặc công cụ xử lý XML của bạn để không chấp nhận hoặc xử lý DTD hoặc thực thể ngoại vi.

3. Đầu vào và kiểm tra dữ liệu đầu vào: Luôn luôn kiểm tra và xác thực dữ liệu đầu vào từ người dùng hoặc nguồn bên ngoài trước khi chấp nhận và xử lý nó. Đảm bảo rằng dữ liệu đầu vào không chứa các thực thể ngoại vi hoặc các cấu trúc XML độc hại có thể khai thác lỗ hổng XXE.

4. Giới hạn quyền truy cập và quyền hạn: Thiết lập các quyền truy cập và quyền hạn phù hợp cho ứng dụng và các thành phần xử lý XML. Điều này đảm bảo rằng chỉ có quyền truy cập cần thiết vào các tệp tin, tài nguyên mạng và hệ thống ngoại vi mà ứng dụng cần để hoạt động.








  
  
