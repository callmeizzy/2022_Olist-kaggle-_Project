# 1. OLIST 데이터셋(from Kaggle)을 이용한 비즈니스 개선점 제안
![image](https://user-images.githubusercontent.com/102460827/173281176-a09f1aa2-2a1c-4e9d-b9ad-f3b16bca7754.png)

**★ 제안내용**
1. 셀러 등급화 서비스 
2. 데이터 적재방식 변경 
3. 유통, 물류 문제 개선을 위한 물류 전담 파트너사 및 자체 유통 허브 구축 제안


**★ 분석 방법**
- Skill : Python
- Visualization Tool : Tableau
- API : Wordcloud / Google Translation
- Ideation Tool : Notion /  Miro
- Status : Complete




# 2. Why

2016년부터 2018년까지 브라질의 여러 마켓플레이스에서 이루어진 100,000개의 주문에 대한 정보가 포함되어 있어 이커머스 비즈니스 분석에 용이할 뿐만 아니라 실제 기업 데이터를 활용해 이커머스 및 리테일과 관련된 비즈니스 문제를 정의할 수 있고, 비즈니스 인사이트와 개선점을 도출할 수 있어 해당 데이터셋을 선택하였다

# 3. Purpose
**[브라질 e-commerce 기업 Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) 데이터를 사용하여 
<셀러 / 내부데이터관리 / 고객> 세가지 sector에서의 인사이트를 도출하고자 한다.**

1. 셀러 등급화에 대한 구체적인 대안 제시 
2. 플랫폼 내부적으로 가진 데이터 문제 개선방안을 대시보드 형태로 요약하여 제공
3. 리뷰데이터 분석을 통한 고객 불만사항 파악 및 개선점 제시


# 4. Data Schema
![image](https://user-images.githubusercontent.com/102460827/173338429-97269ee8-28d3-41fa-8191-c20ee39ae04d.png)

![image](https://user-images.githubusercontent.com/102460827/173338444-dd79b486-312e-4ac0-ada3-405736c21194.png)

## 4.1 Table Description ##

**분석에 사용한 테이블은 4개이며 feature 별 의미하는 것들을 서술하였다**

**1. Olist_Sellers**

Feature | Type | Description
---|---|---
seller_id | string | 판매자 고유 아이디 [중복불가 PK]
seller_zip_code_prefix | string | 판매자 우편번호
seller_city | string | 판매자 거주 도시 
seller_state | string | 판매자 거주 주


**2. Olist_Order_Items**

Feature | Type | Description
---|---|---
order_id | string | 주문번호 
order_item_id | string | order_id 안에서 파생된 제품의 고유한 id (반품시 개별관리 위해 생성된 것으로 보임)
product_id | string | 제품 고유 아이디 [중복불가 PK]
seller_id | string | 판매자 고유 아이디 [중복불가 PK]
shipping_limit_date | string | 상품이 배송되어야 하는 날짜 
price | string | 가격
freight_value | string | 운임


**3. Olist_Orders**

Feature | Type | Description
---|---|---
order_id | string | 주문번호
customer_id | string | 고객별 주문번호 [중복불가 PK]
order_status | string | 주문 상태 
order_purchase_timestamp | string | 주문일자
order_approved_at | string | 지불 승인 일자
order_delivered_carrier_date | string | 송장이 나온 날짜 
order_deliverd_customer_date | string | 배송완료일자
order_estimated_delivery_date | string | 배송예정일


**4. Olist_Customers**

Feature | Type | Description
---|---|---
customer_id | string | 고객별 주문번호 [중복불가 PK]
customer_unique_id | string | 고객 고유 계정 아이디  [중복이 허용되는 고유값]
customer_zip_code_profix | string | 고객 우편 번호
customer_city | string | 고객 거주지 (시)
customer_state | string | 고객 거주지 (주)


# 5. How to Run

**★ Exploratory Data Analysis**
```bash
$ olist_seller_analysis.py
$ olist_orders_analysis.py
$ olist_review_analysis.py
```

**★ Visualization**
```bash
$ Pareto analysis with Tableau
```


# 6. SPIs (Selected Problem Investigations)

## 6.1. 셀러 세분화를 통한 우수 셀러 집중관리(Pareto chart with Python and Tableau)  
**★ Suggestion**

RFM 설정을 위한 Q컷 분석을 (Silver, Gold, Platinum) 3구간으로 나누어 진행를 하였으나, 

Platinum 구간 안에서 최상위와 최하위 점수의 gap이 너무 커 3구간 보다 더 세분화 된 5구간 등급(Bronze, Silver, Gold, Platinum, Diamond) 으로 나누어 분석을 재진행하였다.

세분화된 셀러 등급화를 통한 체계적 관리 및 계층별 멤버십, 혜택 제공이 필요하다는 것을 알 수 있다. 

![image](https://user-images.githubusercontent.com/102460827/173348287-90d6efb4-ff3f-45f4-b257-394834919937.png)

![image](https://user-images.githubusercontent.com/102460827/173342419-e7af5b69-b626-4174-8750-736c0a978cde.png)


**★ Key Findings**

상위 10%의 셀러가 전체매출의 60%를 견인하고 있다.

MonetaryValue와 강한 양의 상관 관계가 있는 Frequency를 기준으로 파레토 차트를 생성하였다.

상위 셀러 안에서도 상위 20 % 셀러 ( 전체에서는 4% )가 두드러진 특징을 가진 것을 확인할 수 있다. 

![image](https://user-images.githubusercontent.com/102460827/173342465-3e02b6db-57fe-40b3-90dc-e9edd14865b3.png)



## 6.2. 플랫폼 내부적으로 가진 데이터 문제 개선방안(Internal Data Recommendation)
플랫폼이 실제 Order Phase를 담을 수 있도록 내부 데이터의 직관성을 강화

**★ Suggestion**

취소 시점이 일어난 정확한 단계에 대한 인지가 부족해 진정한 고객인 seller를 위한 정확한 레포트 전달이 불가하다는 결론을 도출하였고, 

내부 데이터의 Order status의 canceled들이 구간별로 다르고 직관적인 단어로 표현될 수 있게 워딩을 변경하였다. 

![image](https://user-images.githubusercontent.com/102460827/173349641-2c3670b9-1d6e-4c64-b26b-bdc451e0981f.png)



**★ Key Findings**

Data가 실제 주문과정의 Sequential한 Phase를 정확하게 반영하고 있지 않다.

컬럼 및 데이터의 의미상 분석을 위해 전체 컬럼 내에 있는 시간 데이터를 하나씩 매칭시켜 실제 주문과정 단계를 파악하고, 

단계별 order_status의 데이터가 정확하게 반영되었는지 파악하였다

![image](https://user-images.githubusercontent.com/102460827/173349795-2399ef76-283b-4346-af80-3640005a61c4.png)



## 6.3. 리뷰데이터 분석을 통한 고객 불만사항 파악 및 개선점 제시 (Logistics Recommendation)
올리스트의 유통, 물류 문제 개선을 위한 물류 전담 파트너사 및 자체 유통 허브 마련 필요하다.


고객이 주문 건에 대해 만족/불만족 했던 주요 원인 파악을 위해 Review Comment 단어 빈도분석 진행하였다.
(포르투갈어 -> 한국어 번역 | 구글 API번역 사용)

리뷰데이터 약 10만건의 번역 API를 진행하기에 시간이 많이 소요되는 문제 발생하였다.
-빠른 번역과 데이터 추출을 위해 만족도 1-5점 구간별로 데이터를 나누고, Data sampling으로 30% 데이터만 추출하여 워드클라우드를 표현하였다.

![image](https://user-images.githubusercontent.com/102460827/173350664-d87a48b7-7a16-425a-b06c-3f80da7aef27.png)

전반적으로 배송과 주문 과정에 대한 언급이 많음을 알 수 있으며, 
고객 만족도 예측을 위해 올리스트는 제품과 주문과정 및 배송에 대해 비즈니스적인 솔루션이 필요하다는 인사이트를 도출하였다.
![image](https://user-images.githubusercontent.com/102460827/173351350-c5ed6b34-143c-488b-a667-cd3851a58b20.png)
![image](https://user-images.githubusercontent.com/102460827/173350893-86605aac-b426-4889-861f-dfb545ecef67.png)
Order Status가 ‘canceled’ (주문취소) 인 데이터 600개 리뷰에서도 주로 배송 문제로 인해 주문을 취소했다는 사실을 파악하였다.


**★ Suggestion**

셀러상품 픽업부터 고객 배송까지 원스탑 솔루션으로 아웃소싱 or 배송 자회사 설립

![image](https://user-images.githubusercontent.com/102460827/173351715-b19f785d-147d-4dee-a407-74b23e532641.png)

**★ Key Findings**

배송문제관련 부정적인 형용사가 다수존재한다.

브라질의 지리적 한계, 교통적 문제


