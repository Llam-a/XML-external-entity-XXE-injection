# Lab: Exploiting XXE using external entities to retrieve files

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

To solve the lab, inject an XML external entity to retrieve the contents of the `/etc/passwd` file

# Overview:

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/ff4a74f6-0ba6-419d-80ca-501b3cfaf5d0)

Ta có form lab như sau. Theo miêu tả cảu lab này, web này có chức năng `check stock`  phân tích đầu vào XML.

Để solve lab này, perform XEE để nhận content của file `/etc/passwd`.

# Soultion:

Đầu tiên ta vào một sản phảm bất kì rồi `check stock`, sau đó sử dụng Burp Suite để intercept.

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/f4e9eec3-2e04-4f47-8bc0-163ecc68ffd1)

Ta thấy có response là 320. Và để ý ở phần request, có một phần được send bằng XML

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/6f35cb50-fe07-4346-98aa-b6cde5e313ec)

Và nếu có xuất hiện XML, ta phải nghĩ đến XXE injection.Ta sử dụng payload như sau:

```xml
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
```

Payload trên, ta tạo một `ENTITY` là `xxe` và sử dụng câu lệnh `SYSTEM` chỉ ra địa chỉ lấy content `/etc/passwd`.Bây giờ ta cần xác định `DOCTYPE` ta tạo ra và `ENTITY` bằng cách thế `numberID` của `productID` bằng `&xxe;`

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/d4f580d5-03b4-4834-8894-db537a0d2dc4)

Vậy là đã solve được lab

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/03cff5d6-36fa-4e6f-8df1-2a4a45e94f66)







