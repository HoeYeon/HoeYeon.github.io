---
layout: post
title:  "ORB SLAM in Indoor navigation"
date:   2018-07-01
excerpt: "Develop indoor navigation"
project: true
tag:
- ORB SLAM
- project
comments: false
---

## 개요
* Indoor Navigation을 만들기 위한 첫번째 관문으로, 기존에 존재하는 ORB SLAM2를 수정하여 map 저장기능을 추가하고 생성된 맵을 바탕으로 사용자의 실시간 좌표값을 구하도록 했다.(++ 첫 연구실 프로젝트이다. ++)

## 개발배경
* 저번에 만들었던 PlaceRecognition를 보완하기 위해서 엘리베이터가 보이지 않을 때도 사용자의 위치 정보를 표시하고자 하였다.
* 기존에 딥러닝 방식을 쓰기에는 연산량이 너무 많아지기 때문에 계속 사용하기에는 어려움이 있었다.
* 그러던 중 교수님께서 SLAM이라는 기술이 있다는 것을 알려주셨고 그 중에서 보편적으로 많이 쓰이는 ORB SLAM2를 사용하기로 했다.

## 진행과정

### `ORB SLAM2 원본 설치`
* [이 곳](https://github.com/raulmur/ORB_SLAM2) 에서 원본을 다운로드 받았고 기타 필요한 프로그램들은 물려받은 가이드파일을 통해 설치를 했다. (정말 딱 설치 가이드라인만 있었다)

<iframe width="560" height="315" src="https://www.youtube.com/embed/c2ii8FVVoC8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<strong> <center> ORB SLAM 원본으로 제공되는 데이터를 사용했다. </center> </strong>

* 원본은 map 저장기능이 없어 기존에 만들었던 map 로드가 불가능하다.

### `Map 저장기능 추가`
* 구글링을 한 결과 [이 곳](https://github.com/Alkaid-Benetnash/ORB_SLAM2)에서 친절하게 저장기능을 구현해놨기에 참고하여 map 저장기능을 추가했다. <br>

* 폴더에 map.bin 파일이 있으면 localization 모드로 작동하고, 없다면 mapping 모드로 실행되도록 했다.


### `사용자 좌표값`
* map 기능과는 다르게 구글링을 해도 찾을 수 없어 직접 내부를 조금 건드려보기로 했다.

![trajectory](https://user-images.githubusercontent.com/35250791/51800099-f2b15b80-226d-11e9-98a1-377c817f5bbf.jpg)
<strong> <center> 기존에 있는 이 기능에서 힌트를 얻었다. </center> </strong> <br>
* ORB SLAM에는 이제까지 지나왔던 경로를 저장하는 기능이 있는데 이걸 이용하여 실시간으로 좌표 값을 표현해주도록 했다.

### `결과`
<iframe width="560" height="315" src="https://www.youtube.com/embed/7WSsxb2IJec" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<strong> <center> 실험환경은 학교 건물 1층 로비이다. </center> </strong>
* 만들어진 map을 기준으로 엘리베이터의 좌표 값을 입력시켜놨고, 현재 사용자의 좌표가 엘리베이터 일정 반경안에 들어가면 위에 text로 표시하도록 만들었다.

## 느낀점
* Multi Thread에 대한 경험이 부족해서 내부를 건드리는건 어려웠지만, 구글링을 통해 많은 도움을 받았다.
* 이렇게 복잡한 프로그램을 만져본다는 것 자체가 매우 부담되는 일이었고 시작한다고 하더라도 과연 내가 만들 수 있을까 라는 의문이 강하게 들었다.<br> 하지만 복잡하고 어려웠던 프로그램을 다룬만큼 성취감도 매우 컸던 프로젝트였다.
* 만든 SLAM을 더 좋게 발전시켜서 안정적인 Indoor Navigation을 만들어보자 ***(to be continued..)***

---
## `추가되는 내용을 여기에 이어서 계속 업데이트 할 예정이다.`
---
# ORB SLAM python binding

## 개요
* ORB SLAM을 python 환경에서 실행해보고 동시에 yolo와 같이 실행시켜 보았다.

## 개발배경
* 그 전에 만들었던 Place Recognition과 연구실에서 개발중인 프로그램은 python으로 만든데 반해 ORB SLAM은 C++로 되어있어 같이 실행시키는게 불가능했다. 그러던 중 구글링을 통해 ORB SLAM의 python 버전이 깃허브에 있는걸 발견하고 한번 도전해보았다.


## `ORB SLAM2 PythonBinding`
* [이 곳](https://github.com/jskinn/ORB_SLAM2-PythonBindings)과 [이 곳](https://github.com/torrvision/pyORBSLAM2) 이렇게 2개를 찾았는데 후자는 먼저 해 본 결과 실행이 되지 않는다.(후자때매 시간을 많이 날려먹었다.)
* 전자는 기본 python만 사용 할 경우SLAM에서 추가로 boost만 설치해주면 실행이 된다.
* 하지만 난 텐서플로와 keras를 사용해야 됐기 때문에 좀 더 신경쓸 부분이 많았다.


일단 기본적으로 리눅스 환경에서 텐서플로를 설치해본 적이 없기때문에 이 부분에서는 석사 형의 도움을 좀 많이 받았다. Nvidia 드라이버부터 cuda, cudnn 등등 설치하는게 일이었다. 또한 알맞은 opencv, python, tensorflow등 버전을 찾기 위해서 OS를 3번정도 갈아엎은거 같다.

## 결과
* 약 1달동안 설치에만 매달려 수 많은 시행착오 끝에 python 환경에서 ORB SLAM을 돌리는걸 성공했다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/obJH284Tdf4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<b> <center> 전에 만들어놨던 ORB SLAM을 Yolo와 함께 돌렸다.</center> </b> <br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/IOBIONeYCAU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<b> <center> 미리 제공되는 데이터셋과 Yolo를 함께 돌려보았다.</center> </b>

## 느낀점
* 한 달 동안 환경세팅만 하면서 이렇다 할 성과가 없다보니 좌절도 많이했다. 그래서 그런지 Yolo와 SLAM이 함께 돌아가는 모습을 봤을 때 이렇게 성취감을 크게 느꼈던 적이 또 언제였나 싶기도 했다.
