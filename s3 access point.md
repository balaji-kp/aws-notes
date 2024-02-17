s3 access point

create user datauser1 with inline policy:

![image](https://github.com/balaji-kp/aws-notes/assets/77058688/56b2ad90-b6ef-4f0e-b8d1-e61b43552071)

![image](https://github.com/balaji-kp/aws-notes/assets/77058688/cbc433e7-8b2a-44af-bd86-52a50bb1d245)

create bucket with prefix

![image](https://github.com/balaji-kp/aws-notes/assets/77058688/e135c478-6e9e-4073-afe3-46bcdc602e1a)

create bucket policy for above created bucket
![image](https://github.com/balaji-kp/aws-notes/assets/77058688/fd74019f-9d34-469d-9f66-c6f304c33577)

create access point
![image](https://github.com/balaji-kp/aws-notes/assets/77058688/01cb4658-76f4-47c4-8fd9-e1184140cfe2)

create access point with below policy
![image](https://github.com/balaji-kp/aws-notes/assets/77058688/7bcb423a-1aff-4c32-a539-c5923769a487)

![image](https://github.com/balaji-kp/aws-notes/assets/77058688/d2179474-d361-46a4-8004-96ac8ef8c946)

now datauser1 ( IAM user ) can upload object to dataset1 via access point only not directly 








