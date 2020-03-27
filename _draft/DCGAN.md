## Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks   :: DCGAN 논문리뷰

> 이 글은 Alec Radford & Luke Metz 가 작성한 [UNSUPERVISED REPRESENTATION LEARNING WITH DEEP CONVOLUTIONAL GENERATIVE ADVERSARIAL NETWORKS](https://arxiv.org/pdf/1511.06434.pdf)의 논문을 바탕으로 쓴 글이며 틀린 부분이 있을 수도 있습니다. 피드백 감사합니다.



저자는 CNN에서 슈퍼바이저는 아웃풋도 잘나오고 주목을 많이 받았지만 

언 슈퍼바이저 쪽에서는 그렇지 못해서 GANs을 접목하여 언슈퍼바이저 쪽에서 성능을 끌어냄

##### 1.  Introduction

방대한 양의 데이터로 학습한 모델은 성공한 연구이며 컴퓨터비전에서는 좋은 결과물을 얻을 수 있는 이점이 존재한다.

>  •  We propose and evaluate a set of constraints on the architectural topology of Convolutional GANs that make them stable to train in most settings. We name this class of architectures Deep Convolutional GANs (DCGAN)
>
>  •  We use the trained discriminators for image classification tasks, showing competitive performance with other unsupervised algorithms.
>
>  •  We visualize the filters learnt by GANs and empirically show that specific filters have learned to draw specific objects.
>
>  •  We show that the generators have interesting vector arithmetic properties allowing for easy manipulation of many semantic qualities of generated samples.

DCGAN을 정의하고  다른 비지도 학습 알고리즘과 비교

CNN 개념도 설명하면 좋을듯

##### 2. Related Work 

###### 2.1 Representation Learning From Unlabeled Data

대표적인 학습법

표현 학습의 고전적인 접근법은 클러스터링 (ex . K-mean 알고리즘)

클러스터링은 classification에 이점을 가짐

이미지 문맥에서 이미지 패치를 계층적 클러스터링을 이용하여  이미지 표현에서 강력한 모델을 학습할 수 있다 .

또 인기 있는 방법은 오토인코더 / 컴포넌트 분할/ 사다리구조 /Deep belief network





###### 2.2 Generating Natural Images

이미지 생성 모델은 두가지로 나뉜다 

1. Parametric (ex MNIST)

   현실에서 쓰기엔 아직 부족한 부분이 많았음

   Variational sampling approach(2013)는 가끔 성공 했음 그러나 이미지가 흐릿해

    iterative forward diffusion process 방법도 존재함(2015)

   GAN은 생성해도 이해할 수 없거나 노이즈가 심해서 알아볼 수 없어

   laplacian pyramid extension은 높은 퀄리티를 보여줬지만 여러개의 모델에서 생성된 노이즈로 인해 물체가 줏대가 없대

   RNN과 deconvolution Network는 약간의 성공을 보여줬지만 지도학습으로 생성된 것보다 이점이 존재하지 않아 .

2. non-parametric

   데이터 베이스에 있는 이미지와 일치할 가능성 있음

    이미지의 일부분과 일치하는 경우

   이미지의 질감을 합성할 경우

   가 존재함

   논 파라믹 모델이 뭐뭐 있을까?
   

###### 2.3 Visualizing the InterNals of CNNS

​	NN의 문제점은 black Box

​	여기서 CNN 개념을 설명하네  ㅇㅋㄷㅋ



### 3. Approach and Model Architecture

​	LAPGAN에 영향을 받아서 더 나은 모델을 개발했다.

​	여기서 CNN 모델은 pooling 층을 stride로 바꾸고

​	fc layer을 제거함

​	왜 제거했을까?

​	Fully connected Layer는 그렇다치고

​	pooling 층은 stride로 바꾼 이유는 뭘까

​	



​	pooling 은 최고값이나 최저값이나 미들값을 뽑는다라고 생각한다면

​	stride 는 필터와 곱연산을 하여 합한 값 



​	Generator :: 1- 100 Z 인풋 => 4차원 텐서 아웃풋

​							CNN ( stride / without FCN)

​	DIscriminator :: 

​				마지막 레이어 flatten [ sigmoid]

​	

![dcgan](C:\Users\USER\Desktop\dcgan.png)

​	3번째 Batch Normalization

​		평균및 단위 분산이 0이되도록 각 단위에 대한 입력을 정규화 시켜줌

​		정규화를 시키면 단일지점으로 학습되는걸 방지할 수 있음

​		제너레이터에 아웃풋 레이어[Tanh]를 제외한 나머지는 ReLU를 사용

​		 디스크리미네이터엔  LeakyReLU 사용

​	



