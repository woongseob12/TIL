# Encryption & Decryption 

Encryption: 암호 키를 사용하여 정보를 의미를 알 수 없는 형식(암호문)으로 변환 하는 것

Decryption: 암호문을 복호 키를 사용하여 원래의 정보로 복원하는 것



![image](https://user-images.githubusercontent.com/55429912/125157333-7264e380-e1a5-11eb-9538-31948a2d9f68.png)



**암호화 종류**

![image](https://user-images.githubusercontent.com/55429912/125158287-02f1f280-e1ab-11eb-919a-aaee19f4cedf.png)



1. **대칭키(비밀키)

   ![image](https://user-images.githubusercontent.com/55429912/125157766-b9ec6f00-e1a7-11eb-96a5-259360c12492.png)

   - 암호화 키 == 복호화 키

   - 가장 보편적으로 쓰이는 암호화 방식으로 현 미국 표준 방식인 AES(Advanced Encryption Standard)

   - AES는 128~ 256 bit의 키를 적용할 수 있어 보안성이 뛰어나며 공개된 알고리즘으로 누구나 사용 가능

   - 암복호화 속도가 빠르지만 상대편도 같은 열쇠를 가지고 있어야 함

     - 전달하는 과정에서 약점이 노출

     

2. **비대칭키**(공개키)

   - 암호화 키 != 복호화 키
   - 암호화를 하면 하나의 키쌍(A, B) 생성
     - A키(공개키)로 암호화한 암호문은 B키(개인키)로만 복호화 가능
     - B키(개인키)로 암호화한 암호문은 A키(공개키)로만 복호화 가능
   - 전달 과정에 문제가 발생하지 않지만, 대칭키 암호화에 비해 속도가 현저하게 느림
   - 중간자 공격(MITM)에 취약

   ![image](https://user-images.githubusercontent.com/55429912/125158156-0769db80-e1aa-11eb-9e0a-9f75199c708d.png)





