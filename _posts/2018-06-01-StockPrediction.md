---
layout: post
title:  "주가 예측하기"
date:   2018-06-01
excerpt: "주식 그래프를 기반으로 주가를 예측해보자"
tag:
- stock
- crawling
- post
comments: false
---

약간의 취미정도로 소량의 돈을 주식에 투자하고 있었는데 문득 주가를 예측하는건 불가능 할까? 라는 생각이 들어서 구글링을 해봤다.
매도량, 매수량 이런 복잡한 개념없이 순수하게 종가 만으로 예측을 하는 프로그램을 구현한 블로그가 있어서 따라해봤다. [링크](https://pinkwink.kr/1040)

![1](https://user-images.githubusercontent.com/35250791/51812848-a2321080-22f6-11e9-98d0-fd7c68f5fe07.JPG)

블로그에선 이런 식으로 제공되는 데이터를 불러서 가져오는데, 이 곳에서는 코스피 정보만 가져올 수 있고 코스닥 정보는 없다.

소량 투자하기에는 코스닥이 수익률이 좋아서 코스닥에 주로 투자하기에(~~그만큼 위험하다~~) 코스닥 정보 가져오는 부분을 직접 만들어보았다.

![stocknum2](https://user-images.githubusercontent.com/35250791/51813994-79147e80-22fc-11e9-849f-8c2f97b73194.JPG)


![num](https://user-images.githubusercontent.com/35250791/51813987-6e59e980-22fc-11e9-8b54-cc1c3911b477.JPG)
일단 이런 식으로 네이버에서 원하는 기업의 코드번호를 입력한다.

![info](https://user-images.githubusercontent.com/35250791/51814074-df010600-22fc-11e9-9b64-2c5668546e6c.JPG)

그런 다음에 이 부분이 추가된 내용이다. 
입력한 기업의 네이버 금융페이지에 들어가서 페이지마다 시간과 종가 정보를 각각 data_lits, temp_list에 집어넣는다. <br>
이 과정을 1p ~ 50p까지 하게되는데, 이 정도 가져오면 500개정도 데이터가 모인다.


![forecast](https://user-images.githubusercontent.com/35250791/51814347-61d69080-22fe-11e9-913e-f679fb8a0544.JPG)
이렇게 모인 데이터를 이용하여 예측을 해보면 같은 결과가 나오게 되는데, 검은색 점들이 실제 값들이고 파란색 실선은 예측 값이다.<br>
코스닥은 워낙 변동이 심한 탓에 정확한 예측이 힘들다는 것을 알 수 있다.
이걸 믿고 투자하기 보다는 참고용으로 보면 괜찮을거 같다.
