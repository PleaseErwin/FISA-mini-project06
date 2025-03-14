# 분산형 DB Sharding 구현

![ppt1](https://github.com/user-attachments/assets/491ed798-e186-4d32-b819-a42431201cda)
mysql에서 range sharding 구현<br>
고객의 카드 사용 현황 데이터를 나이대별로 나누어 저장한다.<br>
1번 컴퓨터에는 2 ~ 30대<br>
2번 컴퓨터에는 4 ~ 50대<br>
3번 컴퓨터에는 6 ~ 70대<br>
4번 컴퓨터에는 80대 + 기타<br>

![ppt2](https://github.com/user-attachments/assets/854cee79-ea09-41e4-b356-69544e2b714d)
원격과 로컬 DB간에 링크를 생성해서 원격 테이블을 로컬처럼 사용할 수 있도록 하는 federated DB 엔진 사용<br>
링크를 만들기 위해서는 메인 컴퓨터와 원격 컴퓨터에 있는 DB 테이블의 스키마가 같아야 한다.<br>
사전에 미리 mysqldump로 생성한 원본 테이블의 스키마 파일을 각 컴퓨터에 scp로 전송하고, ssh 원격 접속하여 빈 테이블을 생성해 주었다.<br>










