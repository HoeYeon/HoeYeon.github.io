---
layout: post
title:  "MonoDepth_Estimation"
date:   2019-02-01
excerpt: "Estimate obeject'depth using mono camera"
tag:
- depth
- deep_learning
- post
comments: false
---

SLAM을 실행하면서 Object를 Detect하는 것 까지는 성공을 했지만 뭔가 아쉬웠다. Object와의 충돌을 방지하기 위하여 Detect를 한 것이었는데 Detect만 하면 거리를 따지지 못하기때문에 위험을 알리기 어려웠다. 그래서 구글링을 해본결과 2017 CVPR 논문중에 mono camera만을 이용하여 depth를 측정하는 것을 발견하여 이를 활용해보고자 했다.
원본 소스코드는 [여기](https://github.com/mrharicot/monodepth) 를 참고했다.

내가 직접 모델을 학습시키기에는 많은 양의 로컬 데이터를 스테레오 카메라로 구하기가 힘들고 해서 미리 학습된 모델을 사용했다.
일단 간단하게 kiiit dataset에서 사진 한 장만을 돌린 결과는 다음과 같다.
<br>
![kitti_origin](https://user-images.githubusercontent.com/35250791/53890708-0cfc0780-406c-11e9-99a5-5e93065cf56b.png)
이렇게 나온 사진을 disparity map이라고 부른다고 한다.
사용한 모델이 kitti로 학습을 시켜서 그런지 결과가 너무 잘 나온다. 눈으로 보기에도 확연하게 depth 구별이 가능하다.
<br>

내가 사용하는 local dataset에 한 장도 돌려보았다.
![local_origin](https://user-images.githubusercontent.com/35250791/53890747-1e451400-406c-11e9-9774-2f6b5f067022.png)
kitti만큼은 아니지만 어느정도 구분이 가능하다.

소스코드가 잘 작동하는걸 확인했으니 어떻게 활용할지 고민을 해봤다. 현재 내가 필요한건 Object의 depth이니 해당 사진에서 Object의 depth 만 뽑아낼 수 있어야 했다.
하지만 사진이 저렇게 바뀐 상태에서 detection이 제대로 작동할리가 없었다.

![1](https://user-images.githubusercontent.com/35250791/53892039-e4294180-406e-11e9-9f2c-01d723033ce6.PNG)
그래서 생각해낸 방법이 detection을 먼저 돌린 뒤 박스를 그리지않고 박스의 좌표들만 가지고 있도록 했다. 그 다음에 이미지를 diparity map으로 변환을 시키고 그 위에 가지고 있는 박스의 좌표로 그려넣어 보았다.
![kitti_box](https://user-images.githubusercontent.com/35250791/53892269-51d56d80-406f-11e9-8d08-e61288191a5b.png)

![local_box](https://user-images.githubusercontent.com/35250791/53892672-12f3e780-4070-11e9-8436-5886f8354f12.png)

그럴듯한 결과가 나왔다.
원래는 이 결과를 사용자에게 특정 RGB값 이상이면(어느정도 빨간색에 가까우면) 위험신호를 알리는 것으로 끝내려고 했다.
하지만 상대적으로 표시를 해준 이 값을 가지고 Object의 절대적인 값은 구할 수 없을까 라는 생각도 들어 추가로 찾아봤다.

이건 좀 시간이 걸렸는데 공식을 찾고 적용하는게 생각보다 어려웠다.
일단 생선된 disparity map에서 disparity값을 이용하여 실제 depth를 구하는 공식이 있었는데
![stereo_depth](https://user-images.githubusercontent.com/35250791/53893376-6f0b3b80-4071-11e9-94a7-465bbcfee178.jpg)
depth = focal length(f) * baseline / disparity(x-x')
focal length 렌즈에서 이미지 센서까지의 거리, baseline은 2개의 카메라 사이의 거리, disparity는 2대의 카메라에서 생성된 이미지 point의 차이 정도로 이해했다.
이 공식을 거치면 disparity map이 depth map으로 바뀐다. 아직도 이 둘의 차이가 헷갈리는데 disparity map은 object가 2개의 카메라로 비춰질때 생기는 차이의 크기만 나타내준거고 depth map은 실제 depth를 가지고 있는 이미지라고 이해했다.


이렇게 구한 depth map을 정규화 과정을 거쳐서 거리로 표시를 해주었다. mono camera만을 이용하면 depth의 max값이 비 정상적으로 튄다고 하여 정규화 과정이 필요했다.
정규화 과정까지 끝내고 만들어진 결과이다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/kRULNzFtw0o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<b> <center>박스옆에 해당 Object의 거리를 표시해주었다.</center></b>

kitti dataset을 하나 골라잡아서 돌려보았다.
아주 먼 거리는 실제 사람이 봐도 헷갈려서 맞는건가 싶긴 하지만 10m이내에 거리는 만족스럽게 보여주는 것을 볼 수 있다.
(SLAM과 함께 돌리기에는 컴퓨터에 성능이 아쉽다.. 너무 느리다)

느낀 점: 프로젝트 진행도중 생긴 문제점에 대해서 하나부터 열까지 스스로 발견하고 해결방법까지 찾아낸 것이 스스로 대견하다.
확실히 이렇게 진행과정을 적어보니깐 생각을 정리하는데도 도움이 많이 되는것 같다. 요새 ROS라는 것에 흥미가 생기기 시작했는데 기회가 되면 공부하면서 글을 올리도록 해봐야겠다.
