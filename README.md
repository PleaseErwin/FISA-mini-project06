# Shaplica


## 🤝 Team Members
| <img src="https://github.com/kcklkb.png" width="200px"> | <img src="https://github.com/SuGeunJee.png" width="200px"> | <img src="https://github.com/PleaseErwin.png" width="200px"> | <img src="https://github.com/unoYoon.png" width="200px"> |
| :---: | :---: | :---: | :---: |
| [김창규](https://github.com/kcklkb) | [지수근](https://github.com/SuGeunJee) | [서소원](https://github.com/PleaseErwin) | [윤원호](https://github.com/unoYoon) |


# 🛠 Tech Stack

|  **분류**   |   **기술 스택**   |
|--------------|-------------|
| **데이터베이스** | ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) 
| **분산 DB 설계** | ![Sharding](https://img.shields.io/badge/Sharding-%23007ACC?style=for-the-badge&logo=databricks&logoColor=white) ![Replication](https://img.shields.io/badge/Replication-%23999999?style=for-the-badge&logo=amazonrds&logoColor=white) |
| **협업툴**     | ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white) ![Notion](https://img.shields.io/badge/Notion-000000?style=for-the-badge&logo=notion&logoColor=white) ![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white) |
| **서버**  | ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) |

## System & Develop Architecture

![image](https://github.com/user-attachments/assets/9c2c2551-7fb8-4a8f-ad3b-963711cd2a05)


## 주제 선정 배경
본 프로젝트는 실제 업무 환경에서 직면한 대용량 데이터 처리 문제를 해결하기 위해 시작되었습니다. 현재 시스템에서 약 540만건의 카드 데이터를 MySQL 쿼리로 처리하는 과정에서 심각한 성능 저하 문제가 발생했습니다.
### 기존 시스템의 한계점
기존의 단일 데이터베이스 구조에서 SELECT 쿼리 실행 시 발생한 문제점

1. 쿼리 응답 시간 증가: 데이터 규모에 따른 응답시간 증가

    - 1만건: 약 0.5초
    - 10만건: 약 3.7초
    - 540만건: 약 8.5초 (사용자 경험에 심각한 영향)


2. 시스템 부하 증가: 대용량 데이터 처리 시 서버 리소스 과부하
3. 사용자 불만 접수: 느린 응답 시간으로 인한 서비스 품질 저하

<img width="1008" alt="image" src="https://github.com/user-attachments/assets/e4c1b9c1-971b-459c-87a4-a34071f2d236" />



### 해결 방향성
Business Research Insights의 시장 조사에 따르면 분산형 데이터베이스 시장은 연평균 10.5%의 성장률(CAGR)을 보이며, 2024년 약 33억 달러에서 2032년 약 70억 달러 규모로 성장할 것으로 전망됩니다. 이러한 시장 동향을 고려하여, 데이터베이스 샤딩(Sharding)과 레플리카(Replica) 기술을 도입해 대용량 데이터 처리 문제를 해결하고자 합니다.

<img width="1016" alt="image" src="https://github.com/user-attachments/assets/96b78d94-7e45-4f64-992c-bae475bc2894" />

<br>

출처 : https://www.businessresearchinsights.com/market-reports/distributed-database-market-113145

### 분산형 데이터베이스는 다음과 같은 핵심 기능과 기대 효과를 제공합니다

#### 핵심 기능
- 대용량 데이터의 빠른 처리: 다수의 서버를 통한 분산 처리로 성능 향상
- 유연한 확장 기능: 데이터 증가에 따른 시스템 확장 용이
- 효율적 자원 관리: 리소스의 최적화된 할당과 관리

#### 기대 효과

- 실시간 처리 보장: 빠른 응답 시간과 안정적인 성능 제공
- 시스템 안정성 향상: 부하 분산을 통한 안정적 운영
- 운영 비용 최적화: 효율적인 시스템 운영으로 비용 절감

<br>

**본 프로젝트를 통해 분산형 데이터베이스 기술을 실제 환경에 적용하여 540만건의 데이터를 효율적으로 처리하고, 사용자 경험을 개선하는 방안을 제시하고자 합니다.**


<br>

## 📚 분산형 데이터베이스 개념 정리

### 📌 분산형 데이터베이스란?

- 하나의 데이터베이스 관리 시스템이 여러 서버에 연결된 저장 장치를 제어하여 데이터를 분산 저장하고 관리하는 구조입니다.

- 확장성과 성능을 높이기 위해 데이터는 여러 서버에 나누어 저장되며, 대용량 처리에 효과적입니다.

### 🔹 파티셔닝 (Partitioning)

- 단일 데이터베이스 내의 데이터를 나누는 기술로, 성능 향상과 관리 편의성을 위한  기법입니다.

- 분산형 데이터베이스에서는 샤딩(Sharding)과 함께 사용되어 데이터를 효과적으로 분산 저장합니다.

#### 🔸 수직형 파티셔닝 (Vertical Partitioning)

- 속성(Column) 기준 분할

- 테이블의 열을 나누어 서로 다른 테이블로 분리

#### 🔸 수평형 파티셔닝 (Horizontal Partitioning)

- 행(Row) 기준 분할

- 전체 데이터를 조건(예: 지역, ID 범위 등)에 따라 여러 테이블로 나누어 저장

### 🔹 샤딩 (Sharding)

- 데이터를 여러 서버에 분산하여 저장하는 기술입니다. 파티셔닝의 일종으로, 분산 데이터베이스의 핵심 개념입니다.

#### 🔸 레인지 샤딩 (Range Sharding)

- 특정 범위(예: 날짜, ID 범위 등) 기준으로 데이터를 분할하여 각 샤드(서버)에 저장

#### 🔸 해시 샤딩 (Hash Sharding)

- 해시 함수(예: hash(ID) % 서버 수)를 사용해 데이터를 균등하게 분산 저장

- 부하 분산 및 확장성에 용이

### 🔹 레플리카 (Replica)

- 하나의 데이터를 여러 서버에 복제하여 저장하는 기술입니다.

- 장애 대응, 고가용성, 백업 목적

- 마스터-레플리카 구조: 마스터 서버에 문제가 생겨도 레플리카 서버를 통해 지속적인 서비스 제공 가능




## 샤딩이란?
샤딩은 각 DB 서버에서 데이터를 분할하여 저장하는 방식이다. 트래픽을 분산하여 DB 서버의 부하를 줄일 수 있다.
<br>

## 샤딩 구조

![ppt1](https://github.com/user-attachments/assets/491ed798-e186-4d32-b819-a42431201cda)
<br>
<b>mysql db 환경에서 range sharding을 구현하려고 한다.</b><br>
<br>

| 1번 컴퓨터 |  2번 컴퓨터 |  3번 컴퓨터 | 4번 컴퓨터|
|:------:|:------:|:------:|:------:|
| 2 ~ 30대 | 4 ~ 50대 | 6 ~ 70대 | 80대 + 기타 |

고객의 카드 사용 현황 데이터를 나이대별로 나누어 저장한다.<br>

![ppt2](https://github.com/user-attachments/assets/854cee79-ea09-41e4-b356-69544e2b714d)
<br>
원격과 로컬 DB간에 링크를 생성해서 원격 테이블을 로컬처럼 사용할 수 있도록 하는 federated DB 엔진 사용<br>
두 DB간에 링크를 만들기 위해서는 메인 컴퓨터와 원격 컴퓨터에 있는 DB 테이블의 스키마가 같아야 한다.<br>
사전에 미리 mysqldump로 생성한 원본 테이블의 스키마 파일을 각 컴퓨터에 scp로 전송하고, ssh 원격 접속하여 빈 테이블을 생성해 준다.<br><br>

## Main Script File
```
# sharding.sh

```
테이블의 데이터가 저장된 ibd 파일의 크기를 2초마다 가져와서 타겟 사이즈인 1.7기가를 넘을 경우 자동으로 서브 스크립트 파일들을 백그라운드로 실행시킨다.

## Sub Script File
```
# shardingN.sh

```
메인 스크립트 파일 내부에서 실행시키는 스크립트로, 메인 DB에 federated 엔진을 탑재한 테이블을 생성하고 connection으로 각각의 원격 DB 테이블들과 연결한 뒤, 레인지 샤딩에 맞게 일정 나이대 범위의 데이터를 삽입한다.
<br><br>

## 조회 성능

<br>

## 레플리카 데모,고도화


### 재해 방지의 관점에서 단순 백업 목적의 레플리카 구현
- mysql 메인 서버에서 mysql replica 서버로 크론탭과 스크립트 활용하여 레플리케이션 진행
  
- 메인 서버 DB와 동일한 스키마의 replica 서버 DB로 540만개 데이터 이동
  
- 스크립트 파일 구조
  <br>(1) DB정보 파일(replicaconfig4.properties)
  <br>보안을 위해 DB정보를 properties에 따로 저장
  <br>![1 db정보파일](https://github.com/user-attachments/assets/8d7655b6-f7b2-4984-8eac-61c99028b498)
  <br>(2) SQL 파일(replica4.sh)
  <br>실제 쿼리를 실행하는 파일
  <br>![2 sql 파일](https://github.com/user-attachments/assets/e9bfda2e-3005-45bd-9aee-9b3d8616fa0f)
  <br>(3) 실행 파일(replicatest.sh)<br>작업소요시간을 기록하며 SQL 파일을 실행
  <br>![3 실행 파일](https://github.com/user-attachments/assets/192efd65-8143-499d-9fe2-30b260b14df2)

- 레플리케이션 실행 결과
  <br>(1)메인서버
  <br>![4 메인서버](https://github.com/user-attachments/assets/4b3b3acb-fc8f-4e82-847d-50e1471844f1)
  <br>(2)replica서버
  <br>![5 replica서버](https://github.com/user-attachments/assets/65ca1a14-7c32-4fbc-9ca0-fc4194918a35)
  <br>(3)스크립트 실행
  <br>![6 스크립트실행](https://github.com/user-attachments/assets/af662d5e-9327-4eee-a3e9-e74a1a29dcaf)
  <br>(4)결과 확인
  <br>![7 결과확인](https://github.com/user-attachments/assets/252ea5a7-453d-4f7a-a25d-415ac9b9d095)

- 크론탭 설정
  <br>특정 시간이 되면 자동으로 실행될 수 있도록 설정
  <br>로그기록을 통해 작업결과 확인 가능
  <br>![8 크론탭설정](https://github.com/user-attachments/assets/0f69a8da-7039-45f4-9b5d-17341d5f4f41)
  <br>![9 크론탭실행로그](https://github.com/user-attachments/assets/f6f23a10-91c0-4f12-896f-427fa5048c32)

### mysql 실시간 데이터 동기화 레플리카 구현
- 메인/replica 서버 cnf파일 설정 설정
  <br>(1)메인 서버 cnf 파일
  <br>메인 서버임을 인식할 수 있는 id값과 replica 서버 지정
  <br>모든 데이터 변경사항이 binary log 파일에 기록되도록 활성화
  <br>(2)replica 서버 cnf 파일
  <br>binary log를 받아 저장하고 처리할 수 있도록 활성화
  <br>![10 메인,replica서버 cnf파일](https://github.com/user-attachments/assets/09264690-32b7-4fb6-a58a-e4ca27f6a6f5)

- 권한을 가진 마스터 계정 생성 및 binary-로그파일명과 위치 확인
- 위 정보 replica 서버에 입력
  <br>![11 메인,replica서버 cnf파일](https://github.com/user-attachments/assets/0c852740-95f2-401f-8b10-e3967d1e775e)
 
- 레플리케이션 실행 결과
<br>(1)현재 replica 서버에 20만개 데이터 존재
<br>![12 실행결과-1](https://github.com/user-attachments/assets/7c190286-3143-4ad5-9c1d-013f2acc6f76)
<br>(2)실시간 데이터 동기화 설정
<br>![13 실행결과-2](https://github.com/user-attachments/assets/bdf9e098-5f16-4b77-8a0a-1e08a7b4ddec)
<br>(3)메인 서버에 10만개 새로운 데이터 입력
<br>![14 실행결과-3](https://github.com/user-attachments/assets/bd86a434-3438-4351-8fbc-d461ce95bddb)
<br>(4)replica 서버에 실시간 데이터 동기화 확인
<br>![15 실행결과](https://github.com/user-attachments/assets/577780ee-c053-48ca-86be-2b2bd3ee720f)
<br>![16 실행결과](https://github.com/user-attachments/assets/e4749320-3991-4a77-a701-5ed0506df7a2)

### 4-3)레플리케이션 후 부하 테스트를 통해 부하 감소 검증
- 메인/replica 서버에 530만개 데이터 입력 후 부하테스트 진행
- 실행 결과
<br>(1) 1개의 DB에 4명이 동시에 동일한 조회 쿼리 테스트
<br>-> 평균 응답시간 약 14초
<br>![17 부하테스트](https://github.com/user-attachments/assets/95f0d49b-9d69-4e22-af62-2b8f2ed51739)
<br>(2) 메인 서버에 2명 / replica 서버에 2명 분산 후 동시에 동일한 조회 쿼리 테스트
<br>-> 평균 응답시간 9초, 5초
<br>![18 부하테스트](https://github.com/user-attachments/assets/b2e37c2a-03ab-4ba1-acbd-656e9f002ccc)

<br>




