# 1. OLIST 데이터셋(from Kaggle)을 이용한 비즈니스 개선점 제안
![image](https://user-images.githubusercontent.com/102460827/173281176-a09f1aa2-2a1c-4e9d-b9ad-f3b16bca7754.png)

[제안내용]
1. 셀러 등급화 서비스 
2. 데이터 적재방식 변경 
3. 유통, 물류 문제 개선을 위한 물류 전담 파트너사 및 자체 유통 허브 구축 제안


[분석 방법]
- Skill : Python
- Visualization Tool : Tableau
- API : Wordcloud / Google Translation
- Ideation Tool : Notion /  Miro
- Status : Complete




# 2. Why

2016년부터 2018년까지 브라질의 여러 마켓플레이스에서 이루어진 100,000개의 주문에 대한 정보가 포함되어 있어 이커머스 비즈니스 분석에 용이할 뿐만 아니라 실제 기업 데이터를 활용해 이커머스 및 리테일과 관련된 비즈니스 문제를 정의할 수 있고, 비즈니스 인사이트와 개선점을 도출할 수 있어 해당 데이터셋을 선택하였다

# 3. Purpose
[브라질 e-commerce 기업 Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) 데이터를 사용하여 

1. 셀러 등급화에 대한 구체적인 대안 제시 
2. 플랫폼 내부적으로 가진 데이터 문제 개선방안을 대시보드 형태로 요약하여 제공
3. 리뷰데이터 분석을 통한 고객 불만사항 파악 및 개선점 제시

위 세가지의 인사이트를 도출하고자 한다.

# 4. Data Schema
![image](https://user-images.githubusercontent.com/102460827/173338429-97269ee8-28d3-41fa-8191-c20ee39ae04d.png)

![image](https://user-images.githubusercontent.com/102460827/173338444-dd79b486-312e-4ac0-ada3-405736c21194.png)


1. Olist_Sellers

Feature | Type | Description
---|---|---
seller_id | string | 판매자 고유 아이디 [중복불가 PK]
seller_zip_code_prefix | string | 판매자 우편번호
seller_city | string | 판매자 거주 도시 
seller_state | string | 판매자 거주 주


2. Olist_Order_Items

Feature | Type | Description
---|---|---
order_id | string | 주문번호 
order_item_id | string | order_id 안에서 파생된 제품의 고유한 id (반품시 개별관리 위해 생성된 것으로 보임)
product_id | string | 제품 고유 아이디 [중복불가 PK]
seller_id | string | 판매자 고유 아이디 [중복불가 PK]
shipping_limit_date | string | 상품이 배송되어야 하는 날짜 
price | string | 가격
freight_value | string | 운임


3. Olist_Orders

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


4. Olist_Customers

Feature | Type | Description
---|---|---
customer_id | string | 고객별 주문번호 [중복불가 PK]
customer_unique_id | string | 고객 고유 계정 아이디  [중복이 허용되는 고유값]
customer_zip_code_profix | string | 고객 우편 번호
customer_city | string | 고객 거주지 (시)
customer_state | string | 고객 거주지 (주)


# 5. How to Run

**Exploratory Data Analysis**
```bash
$ olist_seller_analysis.py
$ olist_orders_analysis.py
$ olist_review_analysis.py
```

**visualization**
```bash
$ Pareto analysis with Tableau
```


# 6. SPIs (Selected Problem Investigations)

## 6.1. 셀러 세분화를 통한 우수 셀러 집중관리(Pareto chart with Python and Tableau)  


사용자별 특성을 파악하기위해 군집 분석을 하였다. 앞서 전처리한 임베딩 벡터를 통해서 k-means 시행했다. 최적의 k를 구하기위해 1부터 9까지 k-means를 실행한 후 clustering 결과마다 Inertia 값을 비교하여 그 차이가 줄어드는 지점의 k로 결정한다.

![image](https://user-images.githubusercontent.com/102460827/173336060-0d9e2ef5-438a-4d42-a63c-aa890f09bc89.png)


적절한 군집수는 6으로 결정했고 각 결과에 대해 시각화하기 위해서 차원축소 방법 중 하나인 주성분분석(Principle Component Analysis)를 사용한다. 임베딩 벡터 차원 수를 시각화할 수 있도록 2차원으로 축소 후 클래스별로 산점도를 그렸다.

군집2의 경우 군집0,3과 유사한 점이 많고 군집 4의 경우 수가 적고 다른 군집과 섞여있었다. 더 정확한 해석을 하기위해 각 군집별 리뷰데이터를 워드클라우드로 확인한다.

<p align="center">
    <img src="https://github.com/DataNetworkAnalysis/Cosmetic-Recommendation-for-Man/blob/master/images/pca_scatter.png?raw=true" width='400'><br>
    <i>Figure 2</i>
</p>

각 군집별 특징을 워드클라우드로 보았을 때 우선 군집 4의 경우 NT(No Token)라는 단어가 가장 크고 단어 수가 비교적 적음을 알 수 있다. 이는 전처리 과정에서 형태소 분석시 추출된 단어가 없는 경우 NT(No Token)로 처리했기 때문이다. 군집4는 제외하고 다른 군집들에 대해서 각각 해석하도록한다.

<p align="center">
    <img src="https://github.com/DataNetworkAnalysis/Cosmetic-Recommendation-for-Man/blob/master/images/class(k=6).png?raw=true"><br>
    <i>Figure 3</i>
</p>

<p align='center'>
    <i><strong>Table 1. 군집해석</strong></i><br>

Name | Description
---|---
**신사의 품격**(군집 0) | 주 키워드는 사용/피부/느낌이며 주로 바르는 화장품과 관련된 내용있었다. 사용감, 즉 촉감에 예민한 사람들을 위한 화장품들이 모여있다. 끈적거림을 싫어하는 사람이라면 이 군집을 화장품을 살펴보도록 하자.
**가뭄의 단비**(군집 1) | 군집 1과 유사해보이지만 촉촉/건조/수분/크림과 같은 키워드가 더 많이 보인다. 리뷰별 상품들을 확인했을 때 주로 피부 유형이 건성인 사람들을 위한 화장품들이 모여있다. 추운 겨울 건조한 피부 때문에 고민이라면 이 군집의 화장품을 보는게 좋다.
**홀애비탈출키트**(군집 2) | 주 키워드는 냄새/향수/아빠/선물 이다. 인상 깊은 리뷰는 "아빠와 남동생이 덕분에 더이상 냄새가 나지않아요" 였다. 지옥철 한가운데에서 유난히 내 주변에만 사람이 한가한편이라면 이 군집에 있는 화장품들을 살펴보는게 좋을듯 하다.
**미용실가지뫄**(군집 3) |주 키워드는 가격/사용/머리/고정 이다. 남자의 생명은 머리라는 말도 있다. 남자들이 가장 많이 찾는 카테고리를 고르자면 헤어스타일링을 빼놓을 수가 없다. 여름에 비바람이 불고 겨울에 찬바람이 불어도 끄떡없는 헤어제품을 원한다면 이 군집에 있는 제품들을 보자.
**피부영세시대**(군집5) | 이 군집은 피부영세시대라 쓰고 피부young세시대 또는 피부0세시대라고 읽는다. 자극에 예민하거나 피부에 트러블이 많아서 고민이 많다면 다시 아기피부로 돌아가기위해 이 군집의 제품들을 보는것을 추천한다.

</p>

## 6.2. 상품 추천(Product Recommendation)

혼자사는 남자들을 위한 향 좋은 화장품을 찾기위해서 **"홀애비 냄새나는 남사친을 위한 향 좋은 제품"** 이라는 문장을 검색해보았다. 주변에 혼자사는 남사친들에게서 이런 생각을 해봤고 선물을 줘야하는 경우가 생겼다면 한 번 쯤 검색해서 괜찮은 제품이 뭐가 있을지 확인해볼 수 있다.

```bash
$ bash test.sh '홀애비 냄새나는 남사친을 위한 향 좋은 제품'
```

주로 향수 관련된 제품들이 많았다. 냄새를 없애는데 가장 좋은 방법인 것 같다. 그러나 가격을 고려했을때 다음에도 또 보고싶은 남사친이 아니라면 선물은 자제하는게 좋을 거 같다.

<p align='center'>
    <i><strong>Table 2. 추천리스트</strong></i><br>

category	|brand	|nb_reviews|	vol_price	|product	|product_url
---|---|---|---|---|---
향초   	| 양키캔들 (YANKEE CANDLE)	|113	|623g39,000원	|미드나잇 쟈스민	|/product/43548
여성향수	| 안나수이 (ANNA SUI)	 | 193|	30ml62,000원	|라뉘드 보헴 오 드 뚜왈렛	|/product/16708
남성향수	| 샤넬 (CHANEL)	|59   |	50ml114,000원	|블루 드 샤넬 오 드 빠르펭|	/product/16788
남성향수	| 샤넬 (CHANEL)	|89  	|100ml140,000원	|알뤼르 옴므 스포츠 오 드 뚜왈렛 스프레이|	/product/3297
남성향수	| 페라리 (Ferrari)  |	206	|40ml45,000원	|스쿠데리아 블랙 EDT	|/product/3338

</p>

## 6.3. Cosmetic Dashboard for Man

<p align="center">
    <img src="https://github.com/DataNetworkAnalysis/Cosmetic-Recommendation-for-Man/blob/master/images/Dashboard/slide1.JPG?raw=true">
</p>

<p align="center">
    <img src="https://github.com/DataNetworkAnalysis/Cosmetic-Recommendation-for-Man/blob/master/images/Dashboard/slide2.JPG?raw=true">
</p>

<p align="center">
    <img src="https://github.com/DataNetworkAnalysis/Cosmetic-Recommendation-for-Man/blob/master/images/Dashboard/slide3.JPG?raw=true">
</p>
