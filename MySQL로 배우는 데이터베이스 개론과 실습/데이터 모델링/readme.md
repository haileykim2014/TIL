# Chapter 6 데이터 모델링

**데이터모델링이란 ?**

- 지반 설계를 하는 것
- 현실세계의 복잡한 개념을 단순화하고 추상화시켜 데이터베이스화 하는 과정

**데이터베이스 생명주기**

요구사항 수집 및 분석 → 설계(개념적 모델링 - 논리적 모델링 - 물리적모델링) → 구현 → 운영 의 사이클

**데이터 모델링 과정**

![Untitled]()

**요구사항 수집 및 분석**

- 실제 문서를 수집하고 분석한다.
- 담당자와의 인터뷰나 설문조사를 통해 요구사항을 직접 수렴한다.
- 비슷한 업무를 처리하는 기존의 데이터베이스를 분석한다.
- 각 업무와 연관된 모든 부문을 살펴본다.
1. **개념적 모델링**
    - 개체(entity)를 추출하고 각 개체들 간의 관계(relation)를 정의하여 ER 다이어그램(ERD)을 만드는 과정을 말한다.
    - 개체 : 구체적으로 표현 할 수 있는 실체
    - ER다이어그램 : 이러한 실체들의 관계를 표현한 것
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7627defc-5846-4caa-adb8-4589d03792ab/Untitled.png)
    
2. **논리적 모델링**
    - 개념적 모델링에서 만든 ER 다이어그램을 사용하고자 하는 DBMS에 맞게 사상(매핑)하여 실제 데이터베이스로 구현하기 위한 모델을  만드는 과정이다.
    - 개념적 모델링에서 추출하지 않았던 상세 속성들을 모두 추출 한다.
    - 정규화를 수행한다.
    - 데이터 표준화를 수행한다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1dd3fd0-a9ca-4b76-a47e-fb3332382845/Untitled.png)
    
3. **물리적 모델링**
    - 논리적 모델을 실제 컴퓨터의 저장 장치에 저장하기 위한 물리적 구조를 정의하고 구현하는 과정이다.
    - DBMS의 특성에 맞게 저장 구조를 정의해야한다.
    - 응답시간을 최소화해야 한다.
    - 얼마나 많은 트랜잭션을 동시에 발생시킬 수 있는지 검토해야 한다.
    - 데이터가 저장될 공간을 효율적으로 배치해야 한다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcd2904b-b962-4c8f-81d4-d8cbe9abdf2d/Untitled.png)
    

### ER 모델

- 개념적 모델링에 사용하는 모델
- ER 모델은 세상의 사물을 개체와 개체 간의 관계로 표현한다.
- 데이터 모델링 과정 중 개념적 모델링 단계에 사용하는 모델로 1976년 피터 첸(Peter Chen)이 제안
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/524a4325-2a9c-430d-8b86-67cde9a67061/Untitled.png)
    
- 우리는 위와 같은 E-R 모델로 개념적 모델링(E-R Diagram 생성)을 할 수 있다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1febfd27-b4ea-43c5-91c3-7a99aabcd92a/Untitled.png)
    
- 직원 개체는 프로젝트 개체와 1:N의 작업 관계를 맺고 있으며 각 개체마다 고유한 특성을 나타내는 속성이 있다.
- 개념적 모델링 단계에서 사용하기 때문에 특정 데이터 모델이나 DBMS와 무관하게 설계 할 수 있다.

**ER 다이어그램**

1.  **개체와 개체 타입**
    - 개체 (entity) : 사람, 사물, 장소, 개념, 사건과 같이 유무형의 정보를 가지고 있는 독립적인 실체
    - 개체 : 축구아는 여자, 축구의 이해, 축구의 역사 (마당 서점에서 판매하고 있는 도서들)
    - 개체는 요구사항 수집 및 분석 단계에서 만들어진 요구사항 명세서를 통해 도출된다.
    - E-R Diagram에서 직사각형으로 표시
    - 개체의 특징
        1. 유일한 식별자에 의해 식별이 가능하다.
        2. 꾸준한 관리를 필요로 하는 정보
        3. 두 개이상 영속적으로 존재
        4. 업무 프로세스에 이용
        5. 반드시 자신의 특징을 나타내는 속성을 포함
        6. 다른 개체와 최소 한 개 이상의 관계를 맺음
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e973e52-156e-4435-a072-40b6eb2405dd/Untitled.png)
        

**속성**

- 속성(Attribute) : 개체(Entity)가 가진 성질
- 타원으로 표기하고, 속성이 개체를 유일하게 식별할 경우 밑줄

| 개체 타입 | 속성 |
| --- | --- |
| 도서 | 도서이름, 출판사, 도서단가 |

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/111e8341-a97a-4b2e-ad1c-43c70ba0d22a/Untitled.png)

**관계 타입의 ER 다이어그램 표현**

- 개체와 개체 사이의 관계 표현
- 개체 사이의 연관성
- 관계 타입은 마름모로 표현
- 고객이 도서를 구입한다
    - 고객 : 개체
    - 도서 : 개체
    - 구입한다 : 개념
- 도서와 고객은 구매라는 관계
- 학생과 학과는 소속이라는 관계
- 학생과 강좌는 수강이라는 관계

**관계의 대응수(Mapping Cardinality)**

- 관계집합에서 각 개체들이 참여할 수 있는 대응의 개수

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f2fef5c0-5c32-44d8-bd2d-617bef1c7c6f/Untitled.png)

- 개체의 최솟값을 표시하기 위해 E-R 다이어그램에서는 (최소값, 최대값)으로 표기한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b0bc3df-dc5c-4a49-9ce1-8c899cf51cf0/Untitled.png)

- 학과와 학생의 관계는 1개의 학과의 여러 명의 학생이 있울 수 있다. 그리고 학생이 한 명도 없는 학과가 존재 할 수 있다.(0,*) 학생은 반드시 하나의 학과를 가져야 한다. (1,1)

**ISA(수퍼클래스와 서브클래스)**

- 관계상위 개체의 특성에 따라 하위 개체 타입이 결정되는 형태를 말한다.
- 이때 상위 개체 타입을 수퍼클래스, 하위 개체 타입을 서브클래스라고 한다.

**참여 제약 조건**

- 전체 참여와 부분 참여
- 관계에 참여하는 개체 집합의 참여 형태에 따른 제약 조건으로,
개체 집합의 모든 개체들이 관계에 참여하는 조건을 전체 참여라고 한다.
- 전체 참여는 개체 타입과 관계 사이를 두 줄 실선으로 표시한다.
일부만 참여하는 부분 참여의 경우는 일반적인 관계의 표현과 동일하게 단일 실선으로 표시한다.

---

### 연습문제

- **1. 데이터베이스 설계 순서로 옳은 것은?**
    
    ② 요구사항 분석 -> 개념적 모델링 -> 논리적 모델링 -> 물리적 모델링 -> 데이터베이스 구현
    

- **2. ER 모델의 표현방법으로 옳지 않은 것은?**
    
    ③ 속성-오각형
    
    속성은 타원으로 표현된다.
    

- **3. ER모델에 대한 설명으로 옳지 않은 것은?**
    
    ② 일대일 관계 유형만 표현할 수 있다.
    
    1:1, 1:N, N:M 관계 표현이 가능하다
    

- **4. ER 표기법에 대한 설명 중 옳지 않은 것은?**
    
    ③ 복합 속성
    
    이중 타원은 다중값을 나타내는 속성이다. 복합 속성은 여러 속성으로 구성된 속성으로 큰 타원 아래 작은 타원 여러개로 구성된다.
    

- **5. IE표기법에 대한 설명으로 옳지 않은 것은?**
    
    ④ 0(필수적 참여)
    
    O는 부분참여, |은 필수참여를 나타낸다.
    

- **6. 다음 내용을 모두 포함하는 데이터베이스를 설계하시오. 필요하면 몇 가지 가정을 넣을 수 있다.**
    
    **(1) ER다이어그램을 그리시오.**
    
    (근무기록을 약한개체로 볼 경우)
    
    ![https://blog.kakaocdn.net/dn/Nd4VK/btqEPlMe0ko/KlpHDkr3ZZ8sEBCPlLpFc0/img.png](https://blog.kakaocdn.net/dn/Nd4VK/btqEPlMe0ko/KlpHDkr3ZZ8sEBCPlLpFc0/img.png)
    
    **(2) ER다이어그램을 IE표기법으로 변환하여 그리시오.**
    
    ![https://blog.kakaocdn.net/dn/4AmaB/btqEP3qzzcU/TLPnBeceKcKJ2g7Ylib5Dk/img.png](https://blog.kakaocdn.net/dn/4AmaB/btqEP3qzzcU/TLPnBeceKcKJ2g7Ylib5Dk/img.png)
    
    **(3) ER다이어그램을 테이블로 변환하시오.**
    
    부서(부서번호, 이름)
    
    직원(직원번호, 직원이름, 직책, 부서번호(FK))
    
    근무기록(직원번호(FK), 기간, 직책)
    
    부양가족(직원번호(FK), 이름, 나이)
    

- 7. **다음 내용을 모두 포함하는 데이터베이스를 설계하시오. 필요하면 몇 가지 가정을 넣을 수 있다.**
    
    **(1) ER다이어그램을 그리시오.**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/835ba2ee-fea4-40d1-925a-2cfcbc5e11b6/Untitled.png)
    
    **(2) ER다이어그램을 테이블로 변환하시오.**
    
    주차장(일련번호,이름,이취,주차대수,주차증,직원번호(FK))
    
    직원(직원번호,이름,구내전화번호,운전면허번호)
    

- **8. 다음은 고객과 주문에 관한 ER 다이어그램이다. 개체는 고객(Customer), 제품(Product), 주문(Invoice)으로 구성된다. Place관계는 ‘주문한다’를, LineItem은 ‘주문 항목’을 의미한다. 그림에 해당하는 테이블을 작성하시오 (변환된 테이블의 기본키는 밑줄 실선, *외래키*는 *밑줄 점선*으로 표시한다. 기본키인 동시에 외래키일 경우에는 밑줄 실선으로 표시한다. 테이블 변환을 위하여 필요한 사항 중 설명되지 않은 것은 임의로 정하여 설계한다.**
    
    Invoice(Invoice#, TotalPrderAMT, Date, Terms, ShipVia, *Cust#(FK)* )
    
    Customer(Cust#, Crame, Street, City, State, Zip, Phone)
    
    Product(Prod#, StandardPrice, Description)
    
    LineItem(Prod#(FK), Invoice#(FK), SellPrice, Quantity)
