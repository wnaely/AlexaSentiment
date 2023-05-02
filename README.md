![header](https://capsule-render.vercel.app/api?type=waving&color=F49303&height=300&section=header&text=Amazent&fontSize=80&animation=fadeIn&fontAlignY=36&descSize=25&desc=Prediction%20of%20positive%20and%20negative%20Amazon%20user%20reviews&descAlignY=53&fontColor=FFFFFF)

# Amazent <a href="https://www.amazon.com/" target="_blank"><img src="https://img.shields.io/badge/Amazon-F49303?style=for-the badge&logo=Amazon&logoColor=white">
MobileBert를 활용하여 Amazon 사용자 리뷰에서 나타나는 감성을 긍부정으로 예측


## 1. 개요

   * ### 문제정의
 
     현재 우리는 인터넷을 통해 언제 어디서나 쉽게 상품을 구매할 수 있다. 이러한 형태의 상거래를 전자상거래(e-commerce)라고 한다.
  
     <a href="https://www.samsungpop.com/mobile/invest/poptv.do?cmd=fileDown&FileNm=uma_200626.html"><img width="750" alt="e-commerce" src="https://user-images.githubusercontent.com/130523834/235652059-dfc61816-33cc-47cd-8ff4-28ed1d4ec2d1.jpg">
  
     전자상거래는 글로벌 소매유통시장의 20% 이상을 차지하고 있는 주요 유통채널이다. 정보통신기술 발전과 스마트폰 보급 확산, 안전하고 편리한 결제시스템 발달 등으로 전자상거래가 크게 성장하였다. 코로나19가 확산되면서 전자상거래는 핵심적인 쇼핑 수단으로 부상했으며 외출이 제한된 소비자들이 온라인 쇼핑에 눈을 돌리면서 세계 곳곳에서 전자상거래 주문량이 급증했다.
  
     이러한 전자상거래의 발전으로 인해 고객들은 더욱 많은 제품을 쉽게 구매할 수 있게 되었지만, 제품의 질이나 신뢰성 등에 대한 불안감 역시 함께 증가하였다. 이러한 불안감을 해소하기 위해 고객들은 온라인으로 제품 구매 시 상품의 평점과 리뷰를 주로 참고하고 있다. 이에 따라 사용자들은 상품에 대한 자신의 경험을 리뷰로 남겨 다른 고객들에게 도움을 주며, 이는 전자상거래 업체들이 구매 후기 시스템을 운영하고 활용하는 데 큰 역할을 하고 있다.
  
  
  
  
  <img width="500" alt="eMarket" src="https://user-images.githubusercontent.com/130523834/235649002-7b0ee3d7-1905-4264-bc17-ab4a518ab9c4.png">
  
  <a href="https://www.statista.com/statistics/274255/market-share-of-the-leading-retailers-in-us-e-commerce/" rel="nofollow"><img src="https://www.statista.com/graphic/1/274255/market-share-of-the-leading-retailers-in-us-e-commerce.jpg" alt="Statistic: Market share of leading retail e-commerce companies in the United States as of June 2022 | Statista" style="width: 100%; height: auto !important; max-width:1000px;-ms-interpolation-mode: bicubic;"/></a><br />Find more statistics at  <a href="https://www.statista.com" rel="nofollow">Statista</a>

     Amazon은 세계적인 규모를 가진 전자상거래 업체로서, 수많은 제품과 대량의 리뷰 데이터를 보유하고 있다. 이러한 Amazon 리뷰 데이터를 분석하여 제품의 평판을 파악하고, 고객들이 원하는 제품을 더욱 정확하게 추천해주는 것은 아마존뿐만 아니라 온라인 판매 업체에게 매우 중요한 과제이다. 따라서 이번 프로젝트에서는 아마존 리뷰 데이터를 수집하고 감성 분석을 통해 제품에 대한 고객의 평가를 분석하고자 한다.
  
  <hr>
  
  
   * ### 아마존(전자상거래, 인터넷 유통 업체) 플랫폼에서의 리뷰가 갖는 영향
  
   이에 따라 온라인 판매 업체들은 높은 평점과 긍정적인 리뷰를 얻기 위해 노력하고 있다. 
        이처럼 전자상거래는 고객들이 상품을 선택하고 구매하는데 있어서 중요한 역할을 하며 전자상거래 업체들은 고객들의 구매 경험을 개선하기 위해 더욱 발전된 시스템과 기술을 도입하고 있다.
      
      웹을 통한 전자 상거래와 정보 공유가 활발해짐에 따라 상품에 대한 리뷰 문서가 기하급수적으로 증가하였다. 
사용자들은 상품을 구매한 사이트뿐만 아니라 트위터, 블로그, 페이스북과 같은 소셜 미디어를 통해 자연스럽게 의견을 공유하고 상품 구매시 실제적인 도움을 받는다. 
하지만 리뷰 문서의 방대한 양으로 인해 구매 예정자가 모든 리뷰 문서를 읽고 제품에 대한 전체적인 평가를 파악하는 것은 점점 더 어려워 지고 있다. 

      상품에 대한 주요 의견을 효과적인 정보의 형태로 전달하는 것이 실제 구매에 영향을 주기 때문에[1], 전자 상거래 사이트인 Amazon.com은 상품 자체의 정보뿐만 아니라 상품에 대한 리뷰를 효과적으로 전달하는 것에 높은 비중을 두고 있다.
      구체적으로 상품 자체의 만족도 점수와 세부 특징별 점수를 구매자로부터 입력 받고 이들 점수를 종합하여 제공하며, 구매 예정자들이 유용하다고 평가한 리뷰나 상품 특징을 강조하여 표시한다. 
하지만 이 대부분의 과정은 사용자나 시스템 관리자에 의해 수작업으로 진행되기 때문에, 대량의 문서 리뷰를 대상으로 할 때는 효율성과 비용의 문제가 발생한다. 

      이러한 문제를 해결하고자 리뷰 문서에서 의견을 자동으로 추출하고 분석하는 연구가 시도되었다.
대표적으로 자연언어처리 기법이나 기계 학습에 기반하여 의견의 긍정, 부정을 판별하는 연구를 비롯하여, 통계적 분석 기법에 기반하여 상품에 대한 사용자의 점수, 상품 특징 어휘 빈도수로부터 특징 단위의 평가를 도출하는 연구가 진행되었다.

  <hr>
   
  
      

   * ### Amazon Alexa 사용자 리뷰의 영향력
   
      Amazon Alexa 사용자 리뷰는 Alexa를 사용한 사용자들의 경험과 평가를 담고 있는 정보이다. 이러한 리뷰들은 다른 소비자들이 제품을 구매하기 전에 제품에 대한 정보와 평가를 확인할 수 있는 유용한 참고 자료가 된다. 
      
      Amazon Alexa 리뷰는 제품 개발과 개선에도 큰 도움이 된다. 제품에 대한 피드백을 제공하고, 문제점이나 개선사항을 전달함으로써 제품 개발자들은 소비자들의 요구에 더욱 부합하는 제품을 개발할 수 있다. 또한 기업이 제품 마케팅 전략을 수립하는 데에도 활용되는데 제품의 장점이나 단점을 파악하고, 이를 고려하여 마케팅 전략을 수립함으로써 기업은 더욱 효과적인 제품 홍보와 판매를 할 수 있다.
      
      따라서 Amazon Alexa 사용자 리뷰는 소비자들과 기업 간의 소통을 원활하게 하고, 제품의 품질과 개발을 더욱 효율적이게 해주는 중요한 역할을 한다.
      
      
    
## 2. 데이터

   * ### 데이터 출처
      
      이번 프로젝트에서는 Kaggle에서 제공하는 [Amazon Reviews](https://www.kaggle.com/datasets/kritanjalijain/amazon-reviews) 데이터셋을 사용하였다.
      
   * ### 데이터 소개
     
      이 데이터 세트는 Amazon 고객 리뷰, 별점, 리뷰 날짜, 제품 종류 및 피드백과 같은 다양한 Amazon Alexa 제품에 대한 데이터를 포함하고 있다. 
      
      tsv 파일이었던 데이터셋을 보기 쉽게 xlxs 형식의 파일로 전환하였다.
      
      ![image](https://user-images.githubusercontent.com/130523834/232951823-d88dd0da-576c-49e7-8959-6cc858a9710d.png)

       
   ### 입력 - 모델링 - 출력
   
   
   
