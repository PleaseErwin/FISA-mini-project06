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



