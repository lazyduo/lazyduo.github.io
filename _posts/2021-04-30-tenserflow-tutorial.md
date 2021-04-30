---
title: "TensorFlow Tutorial"
date: 2021-04-30 20:29:00 +0900
classes: wide
tags:
    - tech
    - AIML
    - tensorflow
---
TensorFlow 배워보자!

## TensorFlow 설치

`$ pip install tensorflow`

잘 되는 줄 알았으나 샘플코드 실행하면 에러 발생...


    2021-05-01 03:31:39.741247: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'cudart64_110.dll'; dlerror: cudart64_110.dll not found
    
    어쩌구 저쩌구

    2021-05-01 03:31:39.760589: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1766] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
    Skipping registering GPU devices...

    아니 맘대로 스킵하지 말라고..

위 얘기는 대충 GPU에 맞는 library `.dll`이 없다는 건데, 설치 가이드를 아무리 읽어봐도 잘 이해가 되지 않는다. 난 분명 튜토리얼 대로 GPU로 동작 시키기 위해 깔라는 NVIDIA CUDA, cuDNN 다 설치했는데도 뭔가 이상하다.

아무래도 `TensorFlow - CUDA - cuDNN` 들의 버전이 모두 맞아야 하는 것 같아서 제대로 명시된 버전 맞춰서 깔아보았다. 아깐 Successfully 같은건 
없었는데 그래도 뭔가 더 나아진 것 같다. 근데 문제는 아직도 GPU Skip 해버린다.. 
아직 찾을 수 없는 `cusolver64_11.dll`, `cudnn64_8.dll` 다시 한 번 찾아보자


    2021-05-01 03:57:34.990431: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library cudart64_110.dll
    2021-05-01 03:57:35.024535: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library cublas64_11.dll
    2021-05-01 03:57:35.024892: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library cublasLt64_11.dll
    2021-05-01 03:57:35.041351: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library cufft64_10.dll
    2021-05-01 03:57:35.048298: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library curand64_10.dll
    2021-05-01 03:57:35.051251: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'cusolver64_11.dll'; dlerror: cusolver64_11.dll not found
    2021-05-01 03:57:35.063360: I tensorflow/stream_executor/platform/default/dso_loader.cc:53] Successfully opened dynamic library cusparse64_11.dll
    2021-05-01 03:57:35.066483: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'cudnn64_8.dll'; dlerror: cudnn64_8.dll not found

GitHub 제보를 토대로 CUDA 11.1.0v를 깔아보자. (11.3v도 해보고 11.0도 해봤지만 11.1v를 안 해본 내 잘못이다)

    I installed CUDA 10.2 over 11.1 and the problem seems to be resolved:

믿어보자.

도대체 환경 변수를 몇 번을 설정하는지 모르겠지만..끝까지 간다.
