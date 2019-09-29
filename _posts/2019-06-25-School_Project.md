---
layout: post
title:  "너의 시간표가 보여"
date:   2019-06-25
excerpt: "사용자 요구에 맞는 시간표 추천 프로그램"
project: true
tag:
- java
- algorithm
- web
comments: false
---

### 너의 시간표가 보여
학교에서 졸업프로젝트를 하게 됐다.
주제로는 당장 내가 힘들었던 것을 개선해보고자 했다.
학교생활 정규학기 8학기동안 8번의 수강신청을 하게 되는데 이때 시간표 만드는 일이 꽤나 귀찮은 일이었다.
다른 학교는 모르겠지만 우리 학교의 경우 일일이 시간을 비교하면서 짜는게 너무 귀찮고 불편했다.
![why1](https://user-images.githubusercontent.com/35250791/65835782-4c01eb00-e325-11e9-9bc6-23525e5f0165.JPG)
(학교 수강신청 과정)

주제를 정하고 팀원들과 다음과 같이 업무를 나눴다.
![works](https://user-images.githubusercontent.com/35250791/65835818-c0d52500-e325-11e9-9a2e-d79ceb17f6a3.JPG)

여기서 주로 2번째 알고리즘 파트를 담당해서 진행했다.
필터링 작업은 조건문을 통해서 쉽게 구현이 가능했지만 시간표 조합하는 알고리즘 구현하는게 시간이 좀 걸렸다.
검색을 열심히 해본 결과 [이곳](https://www.tuwlab.com/showcase/20026)을 참고해서 구현해 봤다.

백트래킹 알고리즘은 다음과 같은 과정으로 구현했다.
![algorithm](https://user-images.githubusercontent.com/35250791/65836008-4c4fb580-e328-11e9-9aab-b63e05d091e7.JPG)
교양,웹강,전공 각각 요구학점이 다르기 때문에 이 부분 처리해주는게 어려웠다. 이 알고리즘 짜면서 DFS 공부 제대로 한 것 같다.
이 외에도 시간표가 만들어졌을때 어떤 시간표가 더 좋은 시간표인지 가중치 부여하는 작업을 진행했다.
### 실제 구현화면
![1](https://user-images.githubusercontent.com/35250791/65836053-f3345180-e328-11e9-931b-8fe856efd23d.png)
<center>처음 시작화면 </center>
<br>
<br>
![2](https://user-images.githubusercontent.com/35250791/65836085-72c22080-e329-11e9-8ecc-a2ae072fac8d.JPG)
<center>필터 설정 값 입력 </center>
<br>
<br>
![3](https://user-images.githubusercontent.com/35250791/65836106-a735dc80-e329-11e9-92c5-9e8a16eb008e.JPG)
<center>필터 세부설정 </center>
<br>
<br>
![4](https://user-images.githubusercontent.com/35250791/65836124-efed9580-e329-11e9-8b03-2d5e7c215990.JPG)
<center>결과화면 </center>
<center>(계산된 가중치로 비교했을 때 가장 좋은시간표) </center>
<br>
<br>
![5](https://user-images.githubusercontent.com/35250791/65836158-21666100-e32a-11e9-9471-13ab98d5f929.JPG)
<center>가중치 내림차순 top 20 시간표 </center>
<br>
<br>
### 후기
어떻게 보면 사소한거지만 내가 직접 겪은 불편한 점을 조금이나마 개선했다는 점에 대해 만족하고 있다.(막 학기라 내가 쓸일은 없을 것 같다..)<br>
현재는 데이터 로드할 때 컴퓨터에서 저장된 csv파일을 불러오는 방식으로 작동되는데 이 부분을 좀 개선하고 싶다. 비록 내가 앞으로 이 프로그램을 쓸 일이 있을지 모르겠지만 좀 더 개선시켜서 학교 사람들에게 공유해주고 싶다.
