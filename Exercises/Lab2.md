# Lab: Exploiting XXE to perform SSRF attacks

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

The lab server is running a (simulated) EC2 metadata endpoint at the default URL, which is http://169.254.169.254/. This endpoint can be used to retrieve data about the instance, some of which might be sensitive.

To solve the lab, exploit the XXE vulnerability to perform an SSRF attack that obtains the server's IAM secret access key from the EC2 metadata endpoint.

# Overview:

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/da3bba5e-20ba-4da1-bae3-8414ccd9ec3f)

Ta co form lab như sau, theo miêu tả của lab web này đang chạy một server giả lập EC2 metadata  tại endpoint có URL là `http://169.254.169.254/`.Ở endpoint được sử dụng để nhận data từ xa, một vài trong số đó khá nhạy cảm

# Solution:

Mình sẽ làm tương tự những gì đã làm ở lab trước với payload này:

`<!DOCTYPE random [ <!ENTITY ssrf SYSTEM "http://169.254.169.254/"> ]>`

Nếu các bạn thắc mắc ở lệnh SYSTEM tại sao lại có IP đó thì [ở đây](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html) sẽ giải thích cho bạn

Sau đó thì ta làm giống trong cái link mà mình cung cấp

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/fd48bf54-c0e9-49b0-a676-9b40a06f0edd)

Và hiển thị ra `"Invalid product ID: meta-data"` sau đó ta tiếp tục thêm vào cho đến khi ta có access key.

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/4b1145c2-f8f7-40c0-914b-44324c4415af)

Và ta đã solve được lab

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/d3c626b1-c392-4cc1-a238-b5950204d45a)


# Bonus

Mình muốn cho các bạn xem cái này, chúng ta thể làm được gì nếu có cài AWS key đó

Link github mỉnh để [ở đây](https://github.com/streaak/keyhacks#AWS-Access-Key-ID-and-Secret)

