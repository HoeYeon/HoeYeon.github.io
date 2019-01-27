---
layout: post
title:  "ORB SLAM map save"
date:   2018-03-01
excerpt: "import map saving & get user trajectory"
project: true
tag:
- ORB SLAM
- project
comments: false
---

## 개요
* Indoor Navigation을 만들기 위한 첫번째 관문으로, 기존에 존재하는 ORB SLAM2를 수정하여 map 저장기능을 추가하고 생성된 맵을 바탕으로 사용자의 실시간 좌표값을 구하도록 했다.(++ 첫 연구실 프로젝트이다. ++)

## 진행과정

### `ORB SLAM2 원본 설치`
* [이 곳](https://github.com/raulmur/ORB_SLAM2) 에서 원본을 다운로드 받았고 기타 필요한 프로그램들은 물려받은 가이드파일을 통해 설치를 했다.

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
* 이렇게 복잡한 프로그램을 만져본다는 것 자체가 매우 부담되는 일이었고 시작한다고 하더라도 과연 내가 만들 수 있을까 라는 의문이 강하게 들었다.<br> 포기하고 싶은 순간도 있었지만 결국 이렇게 결과물을 만들어내고 나니 앞으로 다른 프로젝트를 진행하는데에 있어서 자신감이 생긴 것 같다.
* 만든 SLAM을 더 좋게 발전시켜서 안정적인 Indoor Navigation을 만들어보자
