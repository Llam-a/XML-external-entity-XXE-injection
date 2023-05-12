# Lab: Blind XXE with out-of-band interaction via XML parameter entities

This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.

To solve the lab, use a parameter entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.

# Overview:

Ta có form lab như sau

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/d58f05c5-eba6-438e-8846-0e346922c0c1)

Ta thấy trong phần POST sau khi "check stock" thì vẫn hiện ra XML. Nhưng ở phần response không có trả lại content của entity.

Vậy thì cách để làm bài này ta sẽ làm out-of-ban và sử dụng Burp collabrator (cái này thì phải crack).Mình sẽ làm cách crack ở đây.

# Solution:

Ban đầu mình có thử In band.Kết quả trả ra lỗi nhưng lỗi không bao gồm entity của ta.

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/0da8cb31-2187-4414-b89d-4f6e2c75b818)

Bây giờ mình sẽ thử thay đổi `<Store Id>`  bằng `& idonotexist` nghĩa là Entity does not exit.

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/af880364-4013-4e37-b03c-2e803a53803a)

Và xuất hiện lỗi `Parsing error`. Giờ chúng ta sẽ sử dụng out-of-band.Ta chỉ cần chỉ ra collabrator server của chúng ta.

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/45d0701a-a045-484f-9cfe-bd5e89c840d8)

Copy đó và dán vào đây

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/80746317-cfd7-488b-bd92-8e2793f342d2)

Sau đó send và ta đã solve được lab này 

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/5b7a7db3-8414-43c6-9988-f276f82705bb)

Và nều nhìn sang phần burp collabrator ta có DNS và http request gửi đến collabrator

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/dd43f543-9a1d-4808-ab3d-17fd9f2d3f8f)





