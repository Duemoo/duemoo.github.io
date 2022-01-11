---
layout: post
title:  "How to Represent Part-Whole Hierarchies In a Neural Network(2021)"
subtitle:   "부제"
categories: AI
tags: papers
comments: true

---

이 논문은 어떤 실험이나 검증이 없이, 아직 존재하지 않는 아키텍쳐에 대한 이론적인 방향성을 제시한다는 점에서 일반적인 논문과는 많이 다르다. 논문의 단독 저자 Geoffrey Hinton은 인공지능을 공부했다면 모두가 한 번은 이름을 들어보았을 이 분야의 거장으로, Hinton은 44페이지에 달하는 이 논문을 통해 본인이 구상해온 GLOM이라는 가상의 아키텍쳐를 소개하고 있다. 이를 통해 그는 카메라의 관점 등의 요인에 관계 없이 이미지를 구성하는 요소들의 part-whole hierarchy를 나타내는 방법을 제시한다.

![Image Alt 구조]({{ site.baseurl }}/assets/img/GLOM_network.png)

GLOM은 기본적으로 주어지는 이미지의 low-level features부터 시작해 이미지 전체의 representation을 얻는 autoencoder의 구조와 유사하다. 다만, GLOM의 경우에는 이미지의 특정 location에 대한 representation을 만들 때, 특정 level의 representation이 이전 time step의 상위 level과 하위 level의 representation의 영향을 모두 받게 된다. 또한, 이러한 방식으로 만들어지는 각각의 representation은 인접한 column들의 representation의 영향도 받는다. 이 구조를 적절히 설계하면, 특정 level에서 같은 feature를 나타내는 인접한 location들은 모두 해당 level에서 동일한 embedding  vector를 갖게 된다(논문에서는 이러한 구조를 island라고 부른다). 그러면, 아래의 그림과 같이 이미지의 part-whole hierarchy를 나타내는 parse tree 형태의 구조를 NN으로 표현할 수 있다는 것이 Hinton의 주장이다. 예를 들면, 얼굴을 지칭하는 part level embedding을 갖는 column들은 하위 level에서 각각 코와 눈을 나타내는 sub-part level embedding을 갖는 column들로 다시 나뉘는 것이다.

![Image Alt 구조2]({{ site.baseurl }}/assets/img/GLOM_rep.png)

GLOM이 갖는 중요한 특성은, 먼저 이미지에서 나타나는 여러 관념들을 hierarchical하게 구성할 수 있다는 것이다. 예를 들어, 사진 속 사람은 머리, 몸통과 사지로 구성되며, 머리에는 다시 눈, 코, 귀, 입이 있다는 식으로 각 층위별 구성요소를 따질 수 있다는 것이다. 이것은 모델의 interpretability를 크게 개선시키는 데 기여할 수 있다. 다음으로, 이러한 part-whole representation의 구성은 사진의 관점에 영향을 받지 않는다. 그림에는 표시되지  않았지만, 각 representation을 얻을 때 column이 위치하는 location에 대한 정보를 담는 고차원 벡터를 함께 활용하여, 인접한 feature들과의 상대적 위치관계를 고려할 수 있기 때문이다. 마지막으로, GLOM은 이러한 part-whole representation을 스스로 construct한다. 이는 특정 관념을 표현하는 capsule들을 미리 지정한 뒤, 이들의 연결을 통해 part-whole representation을 표현하려 한 기존의 시도와 달리 NN을 사용한 학습에 적합하다.

논문을 읽는 내내 인공지능의 학습 문제를 바라보는 거장의 깊은 통찰에 감탄하며 읽었다. 모두가 똑같이 인공지능을 연구하는데, 그 중에서도 Hinton이 그리고 있는 사고의 지평은 가히 독보적이다. GLOM의 설계는 말할 필요도 없고, 논문 중간중간에 GLOM 구조가 갖는 인간 뇌와의 analogy라던가, GLOM과 심리학에서의 게슈탈트 개념과의 연결 등을 논의할 때마다 저자가 얼마나 인공지능의 학습이라는 문제에 대해 다각도에서 깊은 고찰을 해왔는지 알 수 있었다. 학계 최전선에 있는 거장이 평소에 어떤 아이디어를 갖고 있는지 들여다볼 수 있어 즐거운 시간이었다. 앞으로 이런 종류의 논문이 더 활발하게 나왔으면 좋겠다는 생각이 든다.

사실 이 논문은 transformer, autoencoder 등을 비롯해 2020년까지 등장한 인공지능의 다양한 분야에 대한 이해를 기본으로 요구하면서, 인공지능의 새로운 가능성을 깊게  탐구하는 논문이기에 내용이 정말 어렵다. 그래서 필자도 이번에는 간신히 절반 정도의 내용만 이해한 것 같다. 아직 GLOM은 구체적인 학습법도 다뤄지지 않은 상상 속 모델에 가깝기 때문에 가까운 미래에 이 아이디어가 실현되기는 어려워 보이지만, 거장의 깊은 통찰이 담긴 논문인 만큼 나중에 더 깊게 이해하기 위해 revisit하려고 한다.

논문 링크 및 이미지 출처: [https://arxiv.org/abs/2102.12627](https://arxiv.org/abs/2102.12627)
