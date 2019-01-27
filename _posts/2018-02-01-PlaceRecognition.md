---
layout: post
title:  "PlaceRecognition"
date:   2018-02-01
excerpt: "PlaceRecognition with simple classification"
project: true
tag:
- classification
- project
- python
- deeplearning
comments: false
---

## 개요
* 엘리베이터가 사용자를 기준으로 왼쪽, 오른쪽, 가운데 중 어디에 있는지 알려주느 프로그램이다. image classification을 사용했다.

## 진행과정

### `데이터셋 준비`
<figure class="third">
	<img src="https://user-images.githubusercontent.com/35250791/51796885-8e76a380-223d-11e9-8fb6-a1fd07f1ccdb.jpg">
	<img src="https://user-images.githubusercontent.com/35250791/51796886-91719400-223d-11e9-8370-4a3368c92d6f.jpg">
	<img src="https://user-images.githubusercontent.com/35250791/51796887-95051b00-223d-11e9-94bf-f6ba79f87ece.jpg">
	<!--<figcaption>각각 train_set은 1300개, validation_set은 200개씩이다.</figcaption>-->
</figure>
* 학교엘리베이터로 실험을 하고 학습도 하기 위해서 직접 동영상을 찍어온 뒤 프레임 단위로 나눠서 이미지로 만들었다.

![dataset](https://user-images.githubusercontent.com/35250791/51797112-596c5000-2241-11e9-8e5f-f7fc63fa455e.jpg)
* 각각 train_set은 1300개, validation_set은 200개씩 준비했다.

![shuffle](https://user-images.githubusercontent.com/35250791/51797126-73a62e00-2241-11e9-8445-8150372597f2.JPG)
* left, middle, right 순서대로 들어간 데이터를 셔플해줬다.

### `학습 `
* train set 과 validation set을 각각 하나의 라벨당 1300개, 200개씩 설정했다.
* 학습에는 Alexnet을 사용했다. 기존의 Alexnet은 image size가 224x224지만 연산량 초과로 사양에 맞게 100 x 100으로 수정했다.
++ (https://github.com/NVIDIA/DIGITS/issues/291 ++
++ 해당 사이트를 참고했다.) ++
* 노트북 GPU가 지원이 안돼서 CPU로 학습을 시키려니 시간이 오래걸린다. 어쩔 수 없이 자기전에 학습시켜놓고 잠들었다.

### `결과`
![alexnet](https://user-images.githubusercontent.com/35250791/51796898-bfef6f00-223d-11e9-8672-340a7b8a1f2e.JPG)
* 정확도는 약 90퍼 정도로 보인다.
* 실제 다른 층의 엘리베이터로 실험을 하면??
<iframe width="560" height="315" src="//www.youtube.com/watch?v=xSXOvojoRdg" frameborder="0"> </iframe>
* 주변 환경이 조금 달라질때는 오류를 보이지만 학습시킨 부분에 대해서는 만족스러운 결과를 보여준다.

### `느낀점`
* 학습 데이터를 좀 더 포괄적으로 모아서 적용되는 범위를 넓혀보면 어떨까하는 생각이 든다.
* Alexnet을 VGG를 사용해서 학습시키면 정확도가 올라가지 않을까?
* 데이터셋 준비부터 학습까지 처음 스스로 해본 프로젝트라 우여곡절이 많았지만 만족스러운 결과를 보여서 뿌듯하다. 좀 더 발전시켜서 left, middle, right, _none_ 까지 되는 프로그램을 만들어보자
