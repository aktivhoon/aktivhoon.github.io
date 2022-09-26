---
title: Single neuronal predictions of other's beliefs in humans
layout: post
tags: [Neuroscience, Social Learning]
categories: [Paper Review]
date: 2021-01-28 23:35:01 +0900
use_math: true
---


## Task Setting

피험자들은 false-belief task의 verbal 버전을 진행하였다. 

![img1](https://user-images.githubusercontent.com/4964573/106129988-2d736480-61a4-11eb-932c-ba348be277b3.png)

False-belief task는 다른 사람에 대한 이해, 즉 Theory of Mind에 대해 이해하는데 상당히 유용한 task로 오랜시간동안 많은 곳에서 사용되어왔다. Task 자체는 굉장히 conventional method를 썼지만 재밌는 것은 이 실험에 참여한 피험자들에게 multi-electrode microarray를 장착했기 때문에 **single neuron level의 recording이 가능했다**는 점이다.

당연히 아무 문제도 없는 사람들에게 multi-electrode microarray를 장착시키는 것은 윤리적으로도 문제가 있기 때문에 deep brain stimulation 치료를 받기로 예정된 참가자 11명에 대해서 진행하였다. (참고로 피험자들은 7명의 essential tremor, 3명의 Parkinson's disease, 1명의 dystonia로 구성되었다.)

Electrode를 장착할 수 있는 것은 둘째치고, 그렇다면 어디에서 signal을 측정해야할까라는 질문이 당연히 뒤따라온다. 해당 연구에서는 social reasoning과 관련된 것으로 알려진 **dmPFC 영역**에서 측정하였다.

![image](https://user-images.githubusercontent.com/4964573/106131062-88f22200-61a5-11eb-82ad-328fc3d0b3b8.png)

## Other's beleif vs. Physical

![image](https://user-images.githubusercontent.com/4964573/106131378-f43bf400-61a5-11eb-9979-a2c892e91fb5.png)

위 그림에서 볼 수 있듯이 피험자들은 2가지 질문을 받는다: **"사진 상에서 물병이 어디있는지" (physical)** 와 **"Tom은 물병이 어디있다고 생각할지" (other)**. Raster plot에서 볼 수 있듯 질문 이후 physical과 other's belief 모두에 대해서 dmPFC 영역의 neuron들이 반응하는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/4964573/106131951-aa074280-61a6-11eb-95ec-f0f74c7f6710.png)

각 neuron의 response로 other belief를 encoding하는지, physical을 encoding하는지를 예측하는 linear model을 세워보면, 20% (40개 중 8개)의 neuron들이 other belief를 잘 encoding하는 것을 확인할 수 있다.

## Encoding true & false belief

'다른 사람이 생각하는 것'을 encoding하는 것이 single neuron 단위에서 일어난다는 것을 알았으니 다음 질문은 아마 그 belief가 옳을 때와 그를 때도 알 수 있는지일 것이다. 

![image](https://user-images.githubusercontent.com/4964573/106132796-bf30a100-61a7-11eb-9209-d902440cc1db.png)

위의 실험과 동일한 분석방법으로 진행해보면 이 또한 가능하다는 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/4964573/106135817-c5c11780-61ab-11eb-8708-dbb37aab31c4.png)

Physical과 other's beleif에 대한 encoding accuracy를 각 neuron마다 비교해보면 overlap이 되는 경우들이 상당히 적은 것을 볼 수 있다. (Fig a) 이는 달리 말하면 **other's belief를 encoding하는 neuron들은 physical에 대한 encoding을 대부분 하지 않으며, 둘은 독립적인 뉴런들에 의해 encoding된다는 것이다.** 또한 피험자 스스로 가지고 있는 belief와 관련이 없음을 확인하기 위해서 일부 실험에서는 Tom이 문 밖으로 나갔으나 물병을 책상으로부터 치우는 것을 창문 너머로 보았다는 설정을 추가한 후 Tom의 belief를 물어보았다. (aware session) 이 경우에도 false와 true belief에 대한 decoding performance가 유지되어 other's belief를 encoding하는 것임을 다시금 확인하였다.

비슷한 방식으로 self beleif와 other belief에 대한 decoidng performance를 비교한 결과 굉장히 적은 수만 overlap이 되는 것을 통해 physical truth와 마찬가지로 피험자 자신이 가지고 있는 belief와도 관련이 없음을 확인하였다.

## Content encoding of other's belief

다른 사람의 false belief를 이해할 때는 그것이 참인지 거짓인지만을 이해하는 것이 아니라, 정확히 어떤 믿음을 가지고 있는지를 이해할 필요가 있다. 이는 다른 말로 표현하자면 belief의 content를 이해할 수 있어야한다는 말이다. 예를 들어 Tom이 물병이 탁자에 놓여있는지, 찬장에 놓여있는지를 이해하기 위해서는 **'무엇이' '어디에' 있는지를 이해하는 것이 중요**하다. 

![스크린샷 2021-01-28 21 15 00](https://user-images.githubusercontent.com/4964573/106137374-f6a24c00-61ad-11eb-9a2c-8abdd50b8cb1.png)

실제로 encoding한 neuron들이 어떤 content들을 이해하는데 사용되었는지를 보면 재밌는 결과를 확인할 수 있다. **Other's belief인지 아닌지를 encoding하는 뉴런이 따로, true인지 false인지를 encoding하는 뉴런이 따로, location과 identity를 구분하는 것이 따로인 모습을 볼 수 있다.** (Fig c)

또한, other's belief를 올바르게 대답한 경우(주황)과 틀리게 대답한 경우(보라)에 other's belief가 참인지 거짓인지를 encoding하는 정도가 분명하게 차이나는 것을 확인할 수 있다. (Fig d) 이는 즉 이 뉴런들이 단순히 stimuli에서 들어오는 정보를 처리하는 것이 아니라, **정말로 피험자가 other's belief를 잘 예측했는지에 따라 encoding performance가 달라진다는 것을 보여주는 것**이다. 이는 false-true 외에도 location, identity 등 task relevant한 정보들 모두에서 확인되었다.

## 논문에 대한 단상

Single neuron level에서 other's belief를 encoding하는 neuron들이 존재함을 확인하고, 그것이 기존에 social reasoning과 관련된 것으로 알려진 dmPFC에서 나온 것은 상당히 재밌는 결과이다. Observational learning, Theory of Mind 등에 있어서 dmPFC 영역 외에도 premotor, supplementary motor area나 temporoparietal junction 등도 중요한 역할을 하는데 점점 각 영역이 어떤 역할을 하는지가 정교하게 알려질 수 있는 여건이 마련되고 있는 느낌이다.

개인적으로 PMA, SMA는 다른 사람들의 action을 보고 그것을 자신의 action과 연관시키는 imitation learning 느낌과 상당히 관련이 있을 것 같고, dmPFC 영역은 vmPFC, OFC와 함께 일종의 inference에 특화된 영역 같다. vmPFC는 inter-task inference, OFC는 intra-task inference, dmPFC는 inter-personal inference를 하는 것 같다는 생각이 문득 들기는 하는데 좀 더 명확한 근거를 찾아봐야할 것 같다.

아무튼 social learning에 대한 이해도가 높아짐에 따라 자폐증에 대한 computational model을 만들거나, 재밌는 가설들을 생각해낼 수 있는 여건이 늘어날 것으로 기대된다.

## Reference

[1] [Mohsen Jamali, Benjamin L. Grannan, *et al*. Single-neural predictions of other's beliefs in humans. *Nature*  (2021).](https://www.nature.com/articles/s41586-021-03184-0)
