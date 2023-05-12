# Lab: Blind XXE with out-of-band interaction via XML parameter entities

This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.

To solve the lab, use a parameter entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.

# Overview:

Form của challenge như sau 

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/6a31884f-97dc-4e39-8b08-119809905199)

Theo những gì mình viết lí thuyết thì ta chỉ cần thêm kí tự phần trăm thôi, cách làm vẫn tương tự lab trước.

# Solution

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/cbacc380-0fed-4b85-86fe-604fe7a0090a)

Lab đã được solve

![image](https://github.com/Llam-a/XML-external-entity-XXE-injection/assets/115911041/091bd9d3-53a2-4d88-aa67-cde2907baa99)

