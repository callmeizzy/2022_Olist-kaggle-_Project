# 1.OLIST 데이터셋을 통한 비즈니스 솔루션 제안

 **셀러 / 데이터 관리 / 고객&리뷰 , 3가지 sector에서 제안하는 개선점**
  


1. [RFM 분석을 통한 SELLER 별 등급화 차등관리 (Seller Grading Recommendation)]
2. **[플랫폼 내부적 문제 : 데이터 적재 방식 개선 (Internal Data Recommendation)]
3. **[리뷰데이터 분석을 통한 고객 불만 사항 파악 및 물류 차원의 개선점 제시 (Logistics Recommendation)]
---

# 2. DataSet 선정이유

 2016년 ~ 2018년까지 브라질의 여러 마켓 플레이스에서 이루어진  10만 개의 주문 정보가 포함되어 있어  
 이커머스 비즈니스 분석에 용이하며, **실제 기업 데이터를 활용해 이커머스 및 리테일과 관련된 비즈니스 문제를
 정의할 수 있다.** 따라서 비즈니스 인사이트와 개선점을 도출할 수 있어 해당 데이터셋을 선택하였다.

# 3. Business Model 분석
 올리스트는 온라인 판매를 원하는 셀러가 브라질 주요 마켓플레이스에 입점하고 판매부터 배송까지 전 과정을 
 
 간편하게 관리할 수 있는 기능을 제공하는 통합관리 솔루션을 제시하는 사업을 하고 있다. 
 
 제품을 구매하는 일반 고객이 아닌 **셀러로부터 매출이 발생하는 구조**로
 
 **제품 판매 건 당 중개 수수료 / 플랫폼 월 사용료**로  수익을 내는 구조이다.

![image](https://user-images.githubusercontent.com/102460827/180957002-f34dae14-435c-4b49-911f-c219b00740e1.png)

---

# 4. Data Schema

 총 9개의 테이블 52개의 컬럼으로 이루어져 있다. 
 
 주요 테이블은 고객, 주문, 셀러 테이블이며 그 외에도 결제, 상품, 지역, 리뷰 테이블이 있다.

![image](https://user-images.githubusercontent.com/102460827/180957054-0bd8dfdb-ebc4-4ea9-9ab9-1ba02fb3f4e9.png)
![image](https://user-images.githubusercontent.com/102460827/180957066-77168af9-0a7f-45e1-890e-cf12c8c65fd1.png)
![image](https://user-images.githubusercontent.com/102460827/180957076-c08a2feb-ec4d-41ed-a3d9-e2e0b530cfe9.png)

---

# 5. 비즈니스 솔루션 제안

## [제안 1]  RFM 분석을 통한 SELLER 등급화 및 차등 관리

 **올리스트는 RFM 분석을 활용하여 segmentation을 기반으로 한 셀러 별 benefit 차등을 두어야 한다** 
 
 ex)  등급 별 판매 수수료율 차등 혹은 앱 내 제품의 상단 노출과 같은 benefit 제공  
 
셀러를 5 그룹으로 세분화 하면 **최상위  10%**셀러는 전체 판매의 **60.59% , 상위 20%** 셀러는 **82.57%**의 비중을 가지고 있다. 

![image](https://user-images.githubusercontent.com/102460827/180957362-2d8b02a1-0568-486d-b1c8-91e796e6c8d1.png)

![image](https://user-images.githubusercontent.com/102460827/180957374-b5dda19b-ef2c-4194-a480-ebc39416837f.png)

## [문제의식] **seller 데이터 셋에 셀러 등급 컬럼이 부재한 이유는 무엇인가?**

 올리스트에 입점한 seller의 수는 3095명이며, seller table에는 **셀러 등급과 관련한 컬럼이 없다.**

![image](https://user-images.githubusercontent.com/102460827/180957304-4f9c978f-b450-42f5-af99-10b58af73706.png)

![image](https://user-images.githubusercontent.com/102460827/180957322-31e003a2-4857-4684-90d0-30ff47c3679b.png)

## [가설 & 분석 1] **월간 활성화 셀러(MAS)의 수가 적어서 등급을 나누지 않은 것인가? -** MAS (Monthly Active Seller) 분석

 셀러들의 월 별 총 판매량은 지속적으로 증가 추세를 보인다.
 
 셀러가 주 고객인 올리스트가 **플랫폼 이용 수수료를 기반으로 가파른 성장을 하고 있음**을 의미한다.

![image](https://user-images.githubusercontent.com/102460827/180957475-3fa65e02-541a-427d-bd89-9f64eb72f435.png)

![image](https://user-images.githubusercontent.com/102460827/180957498-82be9923-b7d0-4cd0-befc-91841430762e.png)

## [가설 & 분석 2] **셀러의 Retention rate가 낮아서 그런 것인가? - Retention Ratio 분석**

 heatmap이 의미하는 건 셀러들의 **판매 리텐션은 꾸준히 유지되고 있다**는 점이다.

월 별 cohort_ratio의 평균을 구하고 이를 total_retention에 할당한 후 데이터 프레임 및  plot으로 시각화했다. 
 
 셀러 리텐션 그래프 분석결과, 
 
 전체 기간 내 리텐션 비율이 **4~50%정도로 올리스트 플랫폼에 잔존하는 셀러의 비중**도 높다.
 
 **올리스트는 진정한 고객인 셀러의 리텐션을 성공적으로 보유하고 있다.**

[Heatmap CODE]

![image](https://user-images.githubusercontent.com/102460827/180957668-33725d6c-bfb7-4d6d-a02d-5bec6f0e7a2a.png)

![image](https://user-images.githubusercontent.com/102460827/180957538-b25d9817-c8b9-4ccc-bc3e-57639f35dcc4.png)

[Retention Ratio Graph CODE]
![image](https://user-images.githubusercontent.com/102460827/180957686-969ed209-8ff3-4383-b790-41becb51f1e3.png)

![image](https://user-images.githubusercontent.com/102460827/180957603-0b94adf1-aa0c-4e46-9910-10ab43444dda.png)
![image](https://user-images.githubusercontent.com/102460827/180957614-675f4a2b-2a7a-4bb3-9969-d97b58e5081a.png)
![image](https://user-images.githubusercontent.com/102460827/180957634-392979f3-d0a7-4237-b217-9baea5efa5b6.png)



## [가설 & 분석 3] 그렇다면, 셀러를 몇 개의 그룹으로 나누어야 하는가? **- RFM 분석 & Pareto Chart 시각화**

 `Q = 3 (Before)`

 RFM 설정을 위한 Q컷 분석을 (Silver, Gold, Platinum) 3구간으로 나누어 진행를 하였으나, 
 
 특히 Platinum 등급 안에서 Monetary Value의 최상위 / 최하위 값 격차도 컸으며,  
 
 **등급별 표준편차 값이 커 데이터의 분포상태가 고르지 않다고 판단**하여 
 
 **더 세분화** 된 5 등급(Bronze, Silver, Gold, Platinum, Diamond) 으로 나누어 분석을 재 진행하였다

![image](https://user-images.githubusercontent.com/102460827/180957710-cced330b-5691-44ae-859f-7dcbc318f44d.png)

![image](https://user-images.githubusercontent.com/102460827/180959070-a3dc4678-0c59-4e84-832d-fdc3835de0de.png)

![image](https://user-images.githubusercontent.com/102460827/180959086-c1a51d15-1b4b-4f29-9e58-eb249f7b0b15.png)

 `Q = 5 (After)`

 더 세분화** 된 5 등급(Bronze, Silver, Gold, Platinum, Diamond) 으로 나누어 분석을 재 진행하였다.
 
 ****Q = 3 일 때 보다 **표준편차가 더 작아졌고 데이터들이 고르게 분포되었다**는 것을 알 수 있다. 

![image](https://user-images.githubusercontent.com/102460827/180959113-a23a8d35-ecc0-4f1c-9091-e6b33acd61e1.png)

![image](https://user-images.githubusercontent.com/102460827/180959131-e96761b4-fe48-4fd0-b388-f4e8e4236e06.png)

 Tableau를 활용하여 Diamond 등급의 파레토 차트를 그려보았다. (X축 = seller_id / Y축 = MonetaryValue)
 
 **Q = 5 로 나누었을 때 Diamond 등급에서 최하위 셀러의 monetary value의 값은 1,425 이다** 
 
 (Q = 3일 때보다 격차가 더 줄어들었다)

![image](https://user-images.githubusercontent.com/102460827/180959152-11df9b65-9e18-41a6-b7d6-3920236b59a1.png)
 
 **MonetaryValue와 강한 양의 상관 관계가 있는 Frequency**를 기준으로 파레토 차트를 생성
 
** 상위 10% 셀러 안에서도 상위 20% 셀러가 매출을 견인한다.**

![image](https://user-images.githubusercontent.com/102460827/180959174-5d0a2fbb-df4d-47cc-b7d8-ce3c5427a354.png)

![image](https://user-images.githubusercontent.com/102460827/180959209-5857d794-435b-46ae-a3a8-df9b2ceb7374.png)

![image](https://user-images.githubusercontent.com/102460827/180959222-5d00e154-4468-4330-88fd-f989fe6b669e.png)

---

## [제안 2] **플랫폼 내부적 문제 : 데이터 적재 방식 개선 (Internal Data Recommendation)**

 **플랫폼이 실제 Order Phase를 담을 수 있도록 내부 데이터 직관성을 강화해야 한다**
 
 취소 시점이 일어난 정확한 단계에 대한 인지가 부족해 진정한 고객인 seller를 위한 정확한 대시보드 전달이 불가하다는 결론을 도출하였고, 
 
 내부 데이터의 Order status의 canceled 데이터의 입력조건이 주문 흐름 별로 다르기 때문에 직관적인 단어로 워딩을 변경하였다.

![image](https://user-images.githubusercontent.com/102460827/180959246-4a53b53d-d5f9-4933-8f2c-c6ba9ea8a9b6.png)

![image](https://user-images.githubusercontent.com/102460827/180959265-4216864c-930f-4eb2-92b1-8a9ffbbf07dc.png)

## [문제의식] **orders[’order_status] 컬럼의** Data가 실제 주문 과정의 Sequential Phase를 정확하게 반영하고 있지 않다.

 주문취소를 의미하는(‘canceled’) **여러 단계에 동일한 이름으로 산재**되어 있어 고객인 셀러에게 정확한 리포트를  제공할수 없다고 판단하였다. 
 
 **하단의 4개의 구간에서 발생하는 ‘canceled’** 가 실제 주문 phase를 반영할 수 있도록 명칭 재 설정에 대한 needs 존재한다.

![image](https://user-images.githubusercontent.com/102460827/180959290-5019e087-ef24-4625-9f3e-e2469f3fb821.png)

![image](https://user-images.githubusercontent.com/102460827/180959309-a35da879-edcc-418f-b473-2697b27d5c41.png)

![image](https://user-images.githubusercontent.com/102460827/180959326-24aeb710-ea99-4475-a4b5-239a40acf42a.png)

![image](https://user-images.githubusercontent.com/102460827/180959340-123404c0-31b2-43f9-8926-028812bf3108.png)

![image](https://user-images.githubusercontent.com/102460827/180959375-d70c9529-496e-44c6-b902-021a6971cf74.png)

## [분석] 주문 상태가 바뀔 때 마다 order[’order_status] 컬럼 내의 데이터가 어떻게 변하는가  - 시계열 데이터 분석

 **‘order status＇ 컬럼의** 주문 상태를 나타내는 지표는 8가지이며 **주문 상태가 바뀔 때 마다 데이터가 변경된다.** 
 
하나의 주문상태별로 order 전체 데이터 테이블을 보면서 어떤 시점에 해당하는 상태인지 파악하기 위해 **주문 전체 단계에 if 가설을 검증**하는 식으로 EDA 진행하였다. 

 컬럼 및 데이터의 의미상 분석을 위해 전체 컬럼 내에 있는 시간 데이터를 하나씩 매칭시켜 실제 주문 과정 단계를 파악하고, 
 
 단계 별 order_status의 데이터가 정확하게 반영되었는지 탐색하였다

![image](https://user-images.githubusercontent.com/102460827/180959428-0c66e6d6-dcad-4b0d-8cb7-bbaecae469e1.png)

![image](https://user-images.githubusercontent.com/102460827/180959451-80cd242b-6ddd-4154-bea9-7d882c1d1d0e.png)


![image](https://user-images.githubusercontent.com/102460827/180959474-55fa3c85-456f-45bc-9d7a-f6b2b426fd9e.png)

![image](https://user-images.githubusercontent.com/102460827/180959495-f1767ce3-2ae9-4ff7-ad55-0d4d09f24504.png)


---

## [제안 3] **리뷰데이터 분석을 통한 고객 불만 사항 파악 및 물류 차원의 개선점 제시 (Logistics Recommendation)**

 **유통, 물류 문제 개선을 위한 물류 전담 파트너사 및 자체 유통 허브를 마련할 필요가 있다.** 
 
셀러상품 픽업부터 고객 배송까지 원스탑 솔루션으로 아웃소싱 or 배송 자회사 설립의 필요성 대두

## [문제의식] **리뷰길이가 길수록 리뷰 점수가 낮다**

 **리뷰의 길이가 길수록 리뷰의 점수가 낮으며** 고객이 왜 리뷰를 길게 작성했는지에 대한 **이유를 파악해야 한다**

![image](https://user-images.githubusercontent.com/102460827/180959577-056598d3-31e8-40bf-b73d-ed3a89624582.png)

## [분석] 리뷰 스코어 별, 고객은 어떤 평을 남겼을까?

 주문 건에 대한 고객의 만족/불만족 주요 원인 파악을 위해 Review Comment 단어 빈도를 분석했다.
 
 빠른 번역과 데이터 추출을 위해 만족도 1-5점 구간별로 데이터를 나누고, Google Translation API 를 이용하여 포르투갈어 → 영어 → 한국어 순서로 리뷰 번역 작업을 진행했다.

![image](https://user-images.githubusercontent.com/102460827/180959591-c8832d67-dc1c-4f04-9c8a-0dcde6874636.png)

![image](https://user-images.githubusercontent.com/102460827/180959602-e9829001-d634-4abb-8974-d2d171837bc9.png)

 Order Status가 ‘canceled’ (주문취소) 인 데이터 600개 리뷰에서도 주로 배송 문제로 인해 주문을 취소했다
 
 전반적으로 **배송과 주문 과정에 대한 언급이 많음**을 알 수 있으며, 
 
 **고객 만족도 예측을 위해 올리스트는 제품과 주문과정 및 배송에 대한 비즈니스적인 솔루션이 필요하다.**
 
![image](https://user-images.githubusercontent.com/102460827/180959675-95fb9299-47c3-4170-9583-f05a13a17ef6.png)
![image](https://user-images.githubusercontent.com/102460827/180959707-b44baca1-fd05-4917-9ebb-74140c1f3d0c.png)
![image](https://user-images.githubusercontent.com/102460827/180959723-c2f3ccff-1a76-4d4e-90dc-2a07a949c5a0.png)
