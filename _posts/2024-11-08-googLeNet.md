---
title: 합성곱 신경망 - googLeNet inception_module 작동방식 이해하기
search: true
categories: 
  - Deep-learning  
tags:
  - googLeNet
  - keras.layers.Input
  - inception_module
---
합성곱 신경망 중 하나인 googLeNet의 코드 중 inception_module 작동 방식 이해하기 
<br />

# keras.layers.Input
우선 모델 입력층을 만들기 위해 keras.layers.Input(shape=(28, 28, 3))를 호출하면 입력 텐서의 모양이 (None, 28, 28, 3)와 같이 맨 앞의 None값이 꼭 채워지는 이유가 궁금했다.

> keras.layers.Input(shape=(28, 28, 3))를 하면 입력 텐서의 모양이 (None, 28, 28, 3)가 되는 이유는 맨 앞의 None 값이 배치 크기(batch size)를 나타내기 때문입니다.
<br />
shape 매개변수는 각 입력 샘플의 모양만 지정합니다. 예를 들어 (28, 28, 3)은 한 이미지 샘플의 높이와 너비가 28 픽셀이고, 채널이 3개(RGB)인 이미지 형태를 의미합니다.
텐서플로우에서 모델은 한 번에 여러 샘플(배치)을 처리하기 때문에 배치 차원을 추가해 입력 텐서의 전체 모양을 (batch_size, 28, 28, 3)으로 만듭니다.
여기서 batch_size는 고정되지 않고 모델 훈련이나 예측 시점에서 유연하게 결정될 수 있어, 미리 특정 숫자로 고정하지 않고 None으로 설정됩니다.
<br />
즉, (None, 28, 28, 3)의 None은 모델이 한 번에 처리할 입력 샘플의 수를 동적으로 정할 수 있게 하기 위한 것입니다.
<br />
출처: chatGPT

<br />

# inception_module 작동 방식 이해하기
```python
from tensorflow import keras

# x는  keras.layers.Input(shape=(224, 224, 3))와 같다.
def inception_module(x, filters_1x1, filters_3x3_reduce, filters_3x3, filters_5x5_reduce, filters_5x5, filters_pool_proj, name=None, kernel_init='glorot_uniform', bias_init='zeros'):
    conv_1x1 = Conv2D(filters_1x1, (1, 1), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(x)
    conv_3x3_reduce = Conv2D(filters_3x3_reduce, (1, 1), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(x)
    conv_3x3 = Conv2D(filters_3x3, (3, 3), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(conv_3x3_reduce)
    conv_5x5_reduce = Conv2D(filters_5x5_reduce, (1, 1), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(x)
    conv_5x5 = Conv2D(filters_5x5, (5, 5), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(conv_5x5_reduce)
    max_pool = MaxPool2D((3, 3), strides=(1, 1), padding='same')(x)
    pool_proj = Conv2D(filters_pool_proj, (1, 1), padding='same', activation='relu', kernel_initializer=kernel_init, bias_initializer=bias_init)(max_pool)
    output = concatenate([conv_1x1, conv_3x3, conv_5x5, pool_proj], axis=3, name=name)
    
    print('conv_1x1',conv_1x1.shape)
    print('conv_3x3',conv_3x3.shape)
    print('conv_5x5',conv_5x5.shape)
    print('pool_proj',pool_proj.shape)
    # conv_1x1 (None, 28, 28, 64)
    # conv_3x3 (None, 28, 28, 128)
    # conv_5x5 (None, 28, 28, 32)
    # pool_proj (None, 28, 28, 32)
        
    # print(output)
    # (None, 28, 28, 256)
    # 여기서 256은 conv_1x1 채널수(64) + conv_3x3 채널수(128) + conv_5x5 채널수(32) + pool_proj 채널수(32)이다.
    return output
```
<br />

googLeNet에서 inception_module은 다음과 같이 사용된다.
```python
# 시작 부분
x = Conv2D(64, (7, 7), padding='same', strides=(2, 2), activation='relu', name='conv_1_7x7-2', kernel_initializer=kernel_init,
           bias_initializer=bias_init)(img_input)

x = MaxPool2D((3, 3), strides=(2, 2), name='max_pool_1_3x3-2', padding='same')(x)

x = Conv2D(192, (3, 3), padding='same', strides=(1, 1), activation='relu', name='conv_2_3x3-1', kernel_initializer=kernel_init, bias_initializer=bias_init)(x)
x = MaxPool2D((3, 3), strides=(2, 2), name='max_pool_2_3x3-2', padding='same')(x)

#중간 부분 <- 이 부분이 인셉션 모듈이 처음 사용되기 시작하는 부분
x = inception_module(x, 64, 96, 128, 16, 32, 32, name='inception_3a', kernel_init=kernel_init, bias_init=bias_init)
```
<br />

- ps. googLeNet의 전반적 개념이 알고 싶다면 다음 블로그를 참고하자.
  - [googLeNet 개념 정리](https://ikkison.tistory.com/86)