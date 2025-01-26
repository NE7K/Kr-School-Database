## 📝 작품소개

#### 데이터베이스 활용도

|내용|설명|
|---|---|
|학교 운영 상태 분석|학교의 운영 상태(운영, 미운영)를 파악하여 특정 지역이나 전국적으로 운영 중인 학교의 수를 분석할 수 있습니다. 그리고 이 정보를 통해서 학교 운영의 효율성을 평가하고 개선할 수 있습니다.|
|설립 형태 및 설립 일자 분석|학교의 설립 형태(공립, 사립 등)와 설립 일자를 분석하여 특정 시기나 유형의 학교 설립 동향을 파악할 수 있습니다. 이를 이용해서 추가적으로 학교를 설립하거나 기존 학교의 설립 형태를 변환시킬 때 유용한 정보로 사용될 수 있습니다.|
|지역별 학교 분포|지역구 코드와 학교 정보를 종합하여 각 지역별 학교 분포를 시각화하거나 분석할 수 있습니다. 이를 이용해서 특정 지역의 교육 인프라를 평가하고 필요한 시설 및 자원을 배분하고 배치할 수 있습니다.|
|시도교육청 관할 분석|각 학교가 속한 시도교육청 코드를 통해 교육청 관할 내 학교 수를 파악할 수 있습니다. 이를 통해 교육청별 자원 배분의 적절성을 평가하고, 교육청의 효율성을 향상시킬 수 있습니다.|
|위치 기반 분석|학교 위도와 경도 데이터를 활용하여 지도 기반의 분석을 실행할 수 있습니다. 그래서 특정 지역에 학교의 위치를 시각화할 수도 있으며 학교에 대한 접근성을 평가할 수 있습니다. 이를 이용해서 학교의 위치 선정 및 접근성 개선에 도움을 줄 수 있습니다.|

## ✍️ ERD 작성 및 설명

<img src="https://github.com/user-attachments/assets/132aede8-c72f-433a-a23f-5130be66cc42" width="80%" height="80%">

다음은 제가 제작한 데이터베이스의 ERD입니다. 추가적으로, 이후에도 관계 데이터에서도 설명이 되어있기 때문에 간략한 설명만을 담고있습니다. 그림상에는 각 객체별로 속성이 그려져있지 않지만 아래와 같은 속성들을 가지고 있습니다.

 객체 : 학교, 주소, 시도교육청, 교육지원청
 관계 : 위치, 소속, 관리, 지원

- 학교에는 아래와 같은 속성이 있습니다.
 학교ID, 학교이름, 학교유형, 학교설립일, 설립형태, 운영현황, 데이터생성날짜, 데이터갱신날짜

주소에는 아래와 같은 속성이 있습니다.
지번주소, 도로명주소, 위도, 경도

시도교육청에는 아래와 같은 속성이 있습니다.
시도교육청ID, 시도교육청코드, 시도교육청명

교육지원청에는 아래와 같은 속성이 있습니다.
교육지원청ID, 교육지원청코드, 교육지원청명

## 관계 데이터 모델 작성

 데이터베이스는 총 4개의 테이블로 구성되어 있습니다.

<img src="https://github.com/user-attachments/assets/4bc58679-690d-4139-889d-3218f7d9fc6b" width="50%" height="50%">

## 데이터베이스 구축 - 구조와 데이터 사이의 관계

<img src="https://github.com/user-attachments/assets/b35ae4e4-d541-4da5-94f4-c2562507fa38" width="80%" height="80%">

1. 학교 테이블과 주소 테이블의 관계
 학교 테이블의 ‘학교ID’의 주소 테이블의 ‘학교ID’가 1대1 관계를 이루고 있습니다. 왜냐하면, 하나의 학교는 하나의 주소를 지니고 있기 때문입니다.

2. 학교 테이블과 시도교육청 테이블
 - 학교 테이블의 ‘학교ID’와 ‘시도교육청ID’가 다대일 관계를 지니고 있습니다. 왜냐하면, 여러 개의 학교가 하나의 시도교육청에 속할 수 있기 때문입니다. 즉, 여러 학교가 하나의 시도교육청에 소속되어 있지만, 각 학교는 하나의 시도교육청에만 소속될 수 있습니다.

 - 학교 테이블의 ‘시도교육청ID’와 시도교육청 테이블의 ‘시도교육청ID’이 1대1 관계를 이루고 있습니다. 왜냐하면, 시도교육청ID는 시도교육청의 기본키(Primary Key)이기 때문에 학교 테이블과의 관계가 1대1인 것입니다.

3. 학교 테이블과 교육지원청 테이블 관계
학교 테이블의 ‘교육지원청ID’와 교육지원청 테이블의 ‘교육지원청ID’는 1대1 관계를 가지고 있습니다. 교육지원청ID는 교육지원청의 기본키(Primary Key)이기 때문에 학교 테이블과의 관계가 1대1인 것입니다.

4. 시도교육청 테이블과 교육지원청 테이블
시도교육청 테이블의 ‘시도교육청ID’가 교육지원청 테이블의 ‘교육지원청ID’가 1대1 관계로 이어져있습니다. 왜냐하면, ‘시도교육청ID’와 ‘교육지원청ID’가 둘 다 고유한 인덱스 데이터이기 때문입니다.

## 🔨 쿼리 SQL

### 1. 각 학교별 운영현황
<details>
  <summary>각 학교별 운영현황 쿼리</summary>
  <p>학교 이름과 학교 운영 상태에 대한 정보를 사용자에게 제공해줍니다. 이 쿼리를 제작한 이유는 찾고자하는 학교가 현재 운영하고 있는지 운영하고 있지 않는 상태인지를 우선적으로 체크하기 위해서입니다. 해당 쿼리의 SQL 소스는 다음과 같습니다.

```
SELECT 
    [학교 테이블].학교이름, 
    [학교 테이블].운영현황
FROM 
    [학교 테이블];
```

![Image](https://github.com/user-attachments/assets/18f5baa9-6bf4-450f-83bc-8b6d8e43311d)

</p>
</details>
    
### 2. 시도교육청별 유형별 초등학교 및 중학교 수와 분포

<details>
  <summary>시도교육청별 유형별 초등학교 및 중학교 수와 분포 쿼리</summary>
  <p> 각 지역에있는 시도교육청별 초등학교 및 중학교 수를 계산합니다. 그리고 이 정볼를 학교 설립형태로 다시 구분하여 각 지역별로 어떤 유형의 학교가 얼마나 있는지 사용자에게 데이터를 제공합니다. 아래는 SQL 소스이며, 다음은 쿼리 실행 화면입니다.

```
SELECT 
    [시도교육청 테이블].[시도교육청명], 
    SUM(IIF([학교 테이블].[학교유형] = '초등학교', 1, 0)) AS 초등학교수, 
    SUM(IIF([학교 테이블].[학교유형] = '중학교', 1, 0)) AS 중학교수, 
    SUM(IIF([학교 테이블].[학교유형] = '초등학교' AND [학교 테이블].[설립형태] = '공립', 1, 0)) AS 공립초등학교수, 
    SUM(IIF([학교 테이블].[학교유형] = '초등학교' AND [학교 테이블].[설립형태] = '사립', 1, 0)) AS 사립초등학교수, 
    SUM(IIF([학교 테이블].[학교유형] = '중학교' AND [학교 테이블].[설립형태] = '공립', 1, 0)) AS 공립중학교수, 
    SUM(IIF([학교 테이블].[학교유형] = '중학교' AND [학교 테이블].[설립형태] = '사립', 1, 0)) AS 사립중학교수
FROM 
    [학교 테이블] 
INNER JOIN 
    [시도교육청 테이블] 
ON 
    [학교 테이블].[시도교육청ID] = [시도교육청 테이블].[시도교육청ID]
GROUP BY 
    [시도교육청 테이블].[시도교육청명];
```

![Image](https://github.com/user-attachments/assets/06d8b03c-86db-4a15-be98-221df77a0c1f)


</p>
</details>

### 3. 시도교육청별 학교 상세정보
<details>
  <summary>시도교육청별 학교 상세정보 쿼리</summary>
  <p> 이 쿼리는 특정 시도교육청에 속한 학교의 유형과 운영 현황 그리고 주소를 안내해주는 쿼리로 SQL 소스와 실행화면은 다음과 같습니다.

```
SELECT 
    [시도교육청 테이블].[시도교육청명], 
    [학교 테이블].[학교이름], 
    [학교 테이블].[학교유형], 
    [학교 테이블].[운영현황], 
    [주소 테이블].[도로명주소], 
    [주소 테이블].[지번주소]
FROM 
    ([학교 테이블] 
INNER JOIN 
    [주소 테이블] 
ON 
    [학교 테이블].[학교ID] = [주소 테이블].[학교ID]) 
INNER JOIN 
    [시도교육청 테이블] 
ON 
    [학교 테이블].[시도교육청ID] = [시도교육청 테이블].[시도교육청ID]
WHERE 
    [학교 테이블].[학교유형] IN ('초등학교', '중학교')
ORDER BY 
    [시도교육청 테이블].[시도교육청명], 
    [학교 테이블].[학교유형], 
    [학교 테이블].[학교이름];
```

![Image](https://github.com/user-attachments/assets/866c953b-c1dd-455a-91da-14f2e7f75292)

</p>
</details>

### 4. 시도교육청에 속한 교육지원청 목록
<details>
  <summary>시도교육청에 속한 교육지원청 목록 쿼리</summary>
  <p> 이 쿼리는 각 교육청에 속한 교육지원청 목록을 보여줍니다. 그리고 단순히 목록을 보여주는 것이 아니라 중복된 항목들을 제거해서 출력해주는 SQL입니다.

```
SELECT DISTINCT 
    [시도교육청 테이블].[시도교육청명], 
    [교육지원청 테이블].[교육지원청명]
FROM 
    [시도교육청 테이블] 
INNER JOIN 
    [교육지원청 테이블] 
ON 
    [시도교육청 테이블].[시도교육청코드] = [교육지원청 테이블].[시도교육청코드]
GROUP BY 
    [시도교육청 테이블].[시도교육청명], 
    [교육지원청 테이블].[교육지원청명];
```

때문에, SQL을 실행했을 때 아래와 같이 화면이 출력되기까지 조금의 시간이 걸릴 수 있습니다. 왜냐하면, 처리하는 데이터의 양이 많기 때문입니다. 저는 평균적으로 30초가 걸리던 쿼리 실행 시간을 최적화를 통해서 약 평균 20초로 줄였습니다. 

![Image](https://github.com/user-attachments/assets/8e5de5ca-12b3-4688-895e-38e2b85a49e3)

</p>
</details>

### 5. 특정 위치 학교 중 최근 설립된 학교와 해당 학교가 속한 교육지원청 정보 조회
<details>
  <summary>특정 위치 학교 중 최근 설립된 학교와 해당 학교가 속한 교육지원청 정보 조회 쿼리</summary>
  <p> 이 쿼리는 특정 위치 학교 중 최근 설립된 학교와 반대로 설립된지 오랜 시간이 지난 학교에 대한 주소와 교육지원청을 조회하는 쿼리입니다. 아래는 SQL소스입니다.

 ```
SELECT 
    [학교 테이블].학교이름, 
    [학교 테이블].학교설립일, 
    [주소 테이블].도로명주소, 
    [교육지원청 테이블].교육지원청명
FROM 
    ([교육지원청 테이블] 
INNER JOIN 
    [학교 테이블] 
ON 
    [교육지원청 테이블].[교육지원청ID] = [학교 테이블].[교육지원청ID]) 
INNER JOIN 
    [주소 테이블] 
ON 
    [학교 테이블].[학교ID] = [주소 테이블].[학교ID];
```
쿼리를 실행하면 다음과 같이 학교이름, 설립일, 도로명주소, 교육지원청명이 나타나게 됩니다.

![Image](https://github.com/user-attachments/assets/64cc68d1-60a1-4824-98cd-e1fd8bab8e8f)

</p>
</details>

### 6. 학교의 상세정보 조회
<details>
  <summary>학교의 상세정보 조회 쿼리</summary>
  <p>
 이 쿼리는 학교의 상세정보를 조회하는 테이블로 학교이름, 학교유형, 학교설립일, 설립형태, 운영현황, 지번주소, 도로명주소로 구성되어 있습니다. 아래는 SQL소스와 쿼리 실행 화면입니다.

 ```
SELECT 
    [학교 테이블].학교이름, 
    [학교 테이블].학교유형, 
    [학교 테이블].학교설립일, 
    [학교 테이블].설립형태, 
    [학교 테이블].운영현황, 
    [주소 테이블].지번주소, 
    [주소 테이블].도로명주소
FROM 
    [학교 테이블] 
INNER JOIN 
    [주소 테이블] 
ON 
    [학교 테이블].[학교ID] = [주소 테이블].[학교ID];
```

![Image](https://github.com/user-attachments/assets/168dcbf1-db45-45e9-b027-17021f5f3817)

</p>
</details>


## 데이터 폼

### 1. 학교 테이블 폼

<details>
  <summary>학교 테이블 폼 디자인</summary>
  <p>

 학교 테이블의 폼으로 학교 이름, 학교 유형, 학교 설립일, 설립 형태, 운영현황을 보여주고 있습니다. 

   ![Image](https://github.com/user-attachments/assets/7290abd7-cb4c-4571-8538-cd5a759bc760)

  </p>
</details>

### 2. 주소 테이블 폼
<details>
  <summary>주소 테이블 폼 디자인</summary>
  <p>

 주소 테이블 폼입니다. 아래와 같이 학교ID와 지번 주소, 도로명 주소로 구성되어 있습니다.
 
   ![Image](https://github.com/user-attachments/assets/a8c6a127-091f-4dc1-aa12-5784b7f7e055)

  </p>
</details>


### 3. 시도교육청 테이블 폼
<details>
  <summary>시도교육청 테이블 폼 디자인</summary>
  <p>

 아래는 사용자가 보는 테이블 폼입니다. 시도교육청코드와 시도교육청명으로 구성되어 있습니다.
 
   ![Image](https://github.com/user-attachments/assets/edd4b439-389f-4cda-b6af-008b69ec6c3d)

  </p>
</details>

### 4. 교육지원청 테이블 폼

<details>
  <summary>교육지원청 테이블 폼 디자인</summary>
  <p>

   ![Image](https://github.com/user-attachments/assets/3c06acf2-2a45-4cfd-ab20-48ee18ca01b6)

  </p>
</details>

## 쿼리 보고서 폼

 구현한 쿼리 총 6개의 쿼리를 아래와 같이 보고서 형식으로 구성하였으며, 각 쿼리의 정보를 사용자가 쉽게 볼 수 있도록 구현하였습니다.

### 1. 각 학교별 운영 현황 보고서
<details>
  <summary>각 학교별 운영 현황 보고서 사진</summary>
  <p>

![Image](https://github.com/user-attachments/assets/f6535285-8a41-443a-8467-1bfc161cd2c8)
   
  </p>
</details>

### 2. 시도교육청별 유형별 초등학교 및 중학교 수와 분포 보고서

<details>
  <summary>시도교육청별 유형별 초등학교 및 중학교 수와 분포 보고서 사진</summary>
  <p>

![Image](https://github.com/user-attachments/assets/945c88e6-7e64-42ee-910e-272c047fb3f1)
   
  </p>
</details>

### 3. 시도교육청별 학교 상세정보 보고서

<details>
  <summary>시도교육청별 학교 상세정보 보고서 사진</summary>
  <p>

![Image](https://github.com/user-attachments/assets/0256ddce-3d4b-4231-ab1e-6961164778e3)
   
  </p>
</details>

### 4. 시도교육청에 속한 교육지원청 목록 보고서

<details>
  <summary>시도교육청별에 속한 교육지원청 목록 보고서 사진</summary>
  <p>

![Image](https://github.com/user-attachments/assets/212b4ef4-b476-4a0c-b072-f0f378d65c00)
   
  </p>
</details>

### 5. 특정 위치 학교 중 최근 설립된 학교와 해당 학교가 속한 교육지원청 정보 조회 보고서

<details>
  <summary>특정 위치 학교 중 최근 설립된 학교와 해당 학교가 속한 교육지원청 정보 조회 보고서 사진</summary>
  <p>

![Image](https://github.com/user-attachments/assets/a4c7cb75-9644-4866-95bf-ddacd4437fbc)
   
  </p>
</details>

### 6. 학교의 상세정보 조회 보고서

<details>
  <summary>학교의 상세정보 조회 보고서</summary>
  <p>
   
![Image](https://github.com/user-attachments/assets/c2367928-07d3-4a61-9420-b837b116605d)

  </p>
</details>







 
