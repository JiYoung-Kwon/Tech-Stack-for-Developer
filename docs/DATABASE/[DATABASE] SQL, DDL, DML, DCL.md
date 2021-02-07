# [DATABASE] SQL, DDL, DML, DCL

:writing_hand: *Assembled by JiYoung-Kwon (2021-02-01)* 



## 1. SQL (Structured Query Language)

* 관계형 데이터베이스 관리 시스템(RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그램 언어
* 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안
* 데이터베이스로부터 정보를 얻거나 갱신하기 위한 표준 대화식 프로그래밍 언어
* 많은 수의 데이터베이스 관련 프로그램들이 SQL을 표준으로 채택하고 있음

* SQL 문법의 종류 3가지
  * DDL (Data Definition Language - 데이터 정의 언어) 
  * DML (Data Manipulation Language - 데이터 조작 언어)
  * DCL (Data Control Language - 데이터 제어 언어)

<br/>

## 2. DDL (Data Definition Language)

* 데이터 정의 언어

* 테이블이나 관계의 구조를 생성하는데 사용

  * **데이터베이스와 테이블을 생성, 수정, 삭제**하는 등 데이터 전체의 골격을 결정

* | 종류     | 역할                                    |
  | :------- | :-------------------------------------- |
  | CREATE   | 데이터베이스, 테이블 등을 생성하는 역할 |
  | ALTER    | 테이블을 수정하는 역할                  |
  | DROP     | 데이터베이스, 테이블을 삭제하는 역할    |
  | TRUNCATE | 테이블을 초기화 시키는 역할             |

* SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의하거나 변경 또는 삭제할 때 사용하는 언어

* 데이터베이스 관리자나 데이터베이스 설계자가 사용

#### 2-1. 스키마 / 데이터베이스 정의

- 정확한 의미의 스키마와 데이터베이스는 다르지만 MySQL에서는 같은것으로 봄

- 스키마 생성 / 데이터베이스 생성

  - ```
    CREATE SCHEMA 스키마명; 
    CREATE DATABASE 데이터베이스명; 
    ```

- 스키마 삭제 / 데이터베이스 삭제

  - ```
    DROP SCHEMA 스키마명; 
    DROP DATABASE 데이터베이스명; 
    ```

#### 2-2. 테이블 정의

- 테이블 생성

  - ```
    CREATE TABLE 테이블명( 
     컬럼명1 데이터타입 [DEFAULT 형식], 
        컬럼명2 데이터타입 [DEFAULT 형식] 
    ); 
    ```

  - 제약조건

    - PRIMARY KEY : 기본키
      - 기본키 설정
      - PRIMARY KEY = UNIQUE KEY & NOT NULL
    - UNIQUE KEY : 고유키
      - NULL 가능
      - 중복된 값 불가
    - NOT NULL
      - NULL 값을 금지
    - CHECK
      - 입력할 수 있는 값의 범위 등을 제한
      - TRUE 또는 FALSE로 평가할 수 있는 논리식을 지정
      - MySQL에서 적용을 할 수 있지만 데이터의 무결성을 강요하지 않음 => 적용안됨E
    - FOREIGN KEY : 외래키
      - 테이블 간의 관계를 정의하기 위해 다른 테이블의 기본키를 외래키로 지정
      - 외래키 지정시 참조 무결성 제약 옵션 선택 가능

  - ```
    CREATE TABLE 테이블명( 
     컬럼명1 데이터타입 [DEFAULT 형식], 
        컬럼명2 데이터타입 [DEFAULT 형식], 
        UNIQUE INDEX 컬럼명_UNIQUE(컬럼명 ASC), 
        CONSTRAINT 테이블명_PK PRIMARY KEY(컬럼명), 
        CONSTRAINT 테이블명_FK FOREIGN KEY(컬럼명) REFERENCES 상대테이블명(기본키), 
        CONSTRAINT CHK_테이블명 CHECK (논리식) 
    ); 
    ```

  - ```
    CREATE TABLE TEST( 
    NO INT NOT NULL, 
       NO2 INT, 
       NO3 INT, 
       UNIQUE INDEX NO2_UNIQUE(NO2 ASC), 
       CONSTRAINT TEST_PK PRIMARY KEY(NO), 
       CONSTRAINT TEST_FK FOREIGN KEY(NO3) REFERENCES STUDENT(NUM), 
       CONSTRAINT CHK_TEST CHECK(NO>=1) 
    ); 
    ```

- 테이블 수정

  - 컬럼 추가

  - ```
    ALTER TABLE 테이블명 
     ADD 컬럼명 데이터타입; 
    ```

  - 컬럼 삭제

  - ```
    ALTER TABLE 테이블명 
     DROP 컬럼명; 
    ```

  - 컬럼 수정

  - ```
    ALTER TABLE 테이블명 
     MODIFY 컬럼명 데이터타입; 
    ```

  - 컬럼명 수정

  - ```
    ALTER TABLE 테이블명 
     CHANGE 기존컬럼명 새컬럼명 데이터타입; 
    ```

  - 제약조건 추가

  - ```
    ALTER TABLE 테이블명 
     ADD CONSTRAINT 제약조건명 제약조건(컬럼명); 
    ```

  - 제약조건 삭제

  - ```
    ALTER TABLE 테이블명 
     DROP 제약조건명; 
    ```

- 테이블 초기화

  - ```
    TRUNCATE TABLE 테이블명; 
    ```

  - 테이블의 모든 행을 지움

  - 테이블은 유지

- 테이블 삭제

  - ```
    DROP TABLE 테이블명; 
    ```

  - DROP은 테이블 자체를 삭제하고 TRUNCATE는 테이블은 유지하고 데이터들만 삭제

<br/>

## 3. DML (Data Manipulation Language)

* 데이터 조작 언어

* 테이블에 **데이터를 검색, 삽입, 수정, 삭제**하는 데 사용

  * 정의된 DB에 입력된 레코드 조회, 수정, 삭제 등

* | 종류   | 역할            |
  | :----- | :-------------- |
  | SELECT | 데이터 **조회** |
  | INSERT | 데이터 **삽입** |
  | UPDATE | 데이터 **수정** |
  | DELETE | 데이터 **삭제** |

* 데이터베이스 사용자가 응용 프로그램이나 질의어를 통하여 저장된 데이터를 실질적으로 처리하는데 사용하는 언어

* 데이터베이스 사용자와 데이터베이스 관리 시스템 간의 인터페이스 제공

<br/>

## 4. DCL (Data Control Language)

* 데이터 제어 언어

* 데이터의 **사용 권한**을 관리하는 데 사용

  * 데이터베이스에 접근, 객체에 권한을 주는 등

* | 종류     | 역할                                                         |
  | :------- | :----------------------------------------------------------- |
  | GRANT    | 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한을 부여 |
  | REVOKE   | 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한을 박탈, 회수 |
  | COMMIT   | 트랜잭션의 작업이 정상적으로 완료되었음을 관리자에게 알려줌  |
  | ROLLBACK | 트랜잭션의 작업이 비정상적으로 종료되었을 때 원래 상태로 복구 |

* 데이터를 제어하는 언어

* 데이터의 보안, 무결성, 회복, 병행 수행제어 등을 정의하는데 사용

#### 4-1. GRANT

- 사용자에게 권한을 **부여**하는 명령어

- 권한 허용

  - ```
    GRANT 명령어 ON 데이터베이스명.테이블 TO '아이디'@'localhost'; 
    ```

  - '아이디' 사용자에게 데이터베이스명.테이블에서 명령어를 사용할 수 있는 권한을 부여

  - ```
    GRANT ALL ON TEST.* TO 'test'@'localhost'; 
    ```

    - test 사용자에게 TEST 데이터베이스에 있는 모든 테이블의 모든 명령어를 사용할 수 있는 권한을 부여
    - 모든 권한 : SELECT, INSERT, UPDATE, DELETE, CREATE, DROP,REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLE, LOCK TABLES, CREATE VIEW, CREATE ROUTINE, ALTER ROUTINE, EXECUTE, EVENT TRIGGER

  - ```
    GRANT INSERT ON TEST.* TO 'test'@'localhost'; 
    ```

    - test 사용자에게 TEST 데이터베이스에 있는 INSERT 명령어를 사용할 수 있는 권한을 부여

#### 4-2. REVOKE

- 사용자에게 권한을 **회수**하는 명령어

- 권한 회수

  - ```
    REVOKE 명령어 ON 데이터베이스명.테이블 FROM '아이디'@'localhost' 
    ```

  - '아이디' 사용자에게 데이터베이스명.테이블에서 명령어를 사용할 수 있는 권한을 회수

  - ```
    REVOKE ALL ON TEST.* FROM 'test'@'localhost'; 
    REVOKE INSERT ON TEST.* FROM 'test'@'localhost'; 
    ```

#### 4-3. COMMIT

- 작업한 결과를 물리적 디스크로 저장하고, 작업이 정상적으로 **완료**됨을 관리자에게 알려주는 명령어

- ```
  COMMIT; 
  ```

#### 4-4. ROLLBACK

- 작업했던 내용을 원래의 상태로 **복구**하는 명령어

- INSERT, UPDATE, DELETE와 같은 트랜잭션의 작업을 취소

- COMMIT 명령어를 사용하기 이전의 상태만 ROLLBACK 가능

- ```
  ROLLBACK;
  ```

<br/>

## 5. DELETE, TRUNCATE, DROP의 차이

 \- DELETE, TRUNCATE, DROP : 삭제하는 명령어

| 명령어   | 특징                                                         |
| -------- | ------------------------------------------------------------ |
| DELETE   | 데이터는 지워지지만 테이블 용량은 줄어들지 않는다.<br />원하는 데이터만 지울 수 있다.<br />잘못 삭제 한 경우, 삭제한 것을 되돌릴 수 있다. |
| TRUNCATE | 삭제 후, 용량이 줄어들고 인덱스 등도 모두 삭제된다. <br />테이블이 삭제 되지는 않으나 데이터만 삭제한다. <br />선택해서 지울 수 없다. <br />삭제 후 절대 되돌릴 수 없다. |
| DROP     | 테이블 전체를 삭제한다.<br />공간, 객체를 삭제한다.<br />삭제 후 절대 되돌릴 수 없다. |

<br/>

## :page_with_curl: Reference

[[데이터베이스] DML, DDL, DCL이란?](https://cbw1030.tistory.com/71)

[SQL - DDL, DML, DCL](https://stajun.tistory.com/entry/SQL-DDL-DML-DCL)

[[DB] DDL, DML, DCL 이란?](https://brownbears.tistory.com/180)

[SQL DDL, DML, DCL이란?](https://zzdd1558.tistory.com/88)