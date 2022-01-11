---
layout: post
title:  "Deep Metric Learning Using Triplet Network(2014)"
subtitle:   "부제"
categories: AI
tags: papers
comments: true

---


Deep metric learning은 데이터 간의 유사도를 표현할 수 있는 metric function을 neural network로 학습하는 것이다. 즉, feature 사이의 decision boundary를 학습시키는 일반적인 classification과 달리, feature space에서 '유사한 데이터는 가깝고, 유사하지 않은 데이터는 멀리 떨어진' embedding을 갖도록 학습하는 방법이다. 이는 학습 시 아주 제한된 양의 예시만이 주어지는 상황인 few-shot learning에서 효과적으로 사용될 수 있다.

![Image Alt Triplet Network의 구조]({{ site.baseurl }}/assets/img/triplet_network.PNG)

Metric learning을 하기 위해서는, 데이터에서 얻은 representation의 유사도를 어덯게 정의하냐는 것이다. 해당 논문에서는, Siamese network와 같이 Euclidean distance를 유사도 측정 방법으로 채용했다. 그러나, 두 개의 데이터를 비교해 얻은 contrastive loss로 학습하는 Siamese network와 달리, 주어진 데이터를 같은 class에 속하는 데이터, 다른 class에 속하는 데이터와 함께 세 쌍(triplet)으로 묶어 학습하였다. 구체적으로, 아래의 식을 살펴보면 비슷한 데이터는 embedding vector의 거리가 가깝고, 다른 데이터는 embedding vector의 거리가 멀어지게 학습되도록 loss를 설계했음을 알 수 있다.

![Image Alt ]({{ site.baseurl }}/assets/img/triplet_loss.PNG)

실제로 PCA를 사용해 이렇게 학습된 MNIST dataset의 각 데이터의 embedding을 2차원 평면에 나타내면, 같은 class로 분류되는 데이터끼리는 서로 가까운 곳에 위치해 cluster를 이루는 것을 확인할 수 있다.

![Image Alt Triplet Network를 통해 학습된 MNIST dataset의 embedding](/assets/img/triplet_mnist.PNG)

논문 링크 및 이미지 출처: [https://arxiv.org/abs/1412.6622]({{ site.baseurl }}https://arxiv.org/abs/1412.6622)