# Serialization & Deserialization

![image](https://user-images.githubusercontent.com/55429912/127508607-7aec9ff5-9c10-49d7-960f-eb9a69f8ecf9.png)

Serialization(직렬화): 데이터 구조나 객체를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정

Deserialization(역직렬화): 저장된 데이터를 원래의 데이터 구조나 객체 상태로 복원하는 과정



**직렬화가 필요한 이유?**

> 유의미한 데이터를 만들기 위함

1. 값 형식 데이터(Value Type)
   - Stack에 메모리가 쌓여 직접 접근이 가능
2. 참조 형식 데이터(Reference Type)
   - Heap에 메모리가 할당, Stack에서는 해당 Heap 영역의 메모리를 참조하는 구조
   - 실제 데이터 값이 아닌 Heap에 할당되어있는 메모리 번지 주소를 가지고 있기 때문에 저장, 통신에 사용할 수 없음



직렬화를 통해 각 주소값이 가지는 데이터들을 전부 끌어모아서 값 형식(Value Type)데이터로 변환!!

직렬화가 된 데이터들은 언어에 따라서 Text 또는 Binary 등의 형태가 되는데, 이러한 형태가 되었을 때 저장하거나 통신 시 파싱이 가능한 **유의미한 데이터**가 됨.





참조 : https://hub1234.tistory.com/26#:~:text=%EC%A7%81%EB%A0%AC%ED%99%94%EB%A5%BC%20%EC%93%B0%EB%8A%94%20%EC%9D%B4%EC%9C%A0%EB%8A%94,%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC%20%EB%A7%8C%EB%93%A4%EA%B8%B0%20%EC%9C%84%ED%95%A8%EC%9D%B4%EB%8B%A4.