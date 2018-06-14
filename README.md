## 1. 프로젝트 개요

**프로젝트 명**

Efficient Neural Architecture Search for Windows users.

**연구목적**

적절한 뉴럴네트워크를 디자인 하기위해서는 네트워크에 대한 많은 지식과 경험이 필요합니다.

하지만 구글의 AutoML 프로잭트의 결과 나온 ENAS를 사용하면 네트워크에 대한 지식없이도 높은 성능의 뉴럴네트워크를 

손쉽게 디자인 할 수 있는데 현재(2018.06.14) 공개된 ENAS 코드는 다음과 같은 문제가 존재합니다.

1. 네트워크에 데이터를 인가하려면 이미지 파일을 pickle 파일로 변환해주어야 하기때문에 비전공자들이 사용하기 어렵다.

2. 코드가 Ubuntu에서만 실행된다.

3. ENAS의 기존 Code는 Data Augmentation에 관한 기능을 제공하지 않는다.


<br/>따라서 저는 

1. 비전공자들이 사용하기 편하도록 Png파일을 네트워크에 바로 인가할 수 있도록 만들었으며

2. Windows 10에서도 실행 할 수 있고

3. Data Augmentation 코드를 추가하여 더욱 좋은 결과를 얻을 수 있도록 만들었습니다.


## 2. 사용한 데이터셋
- MNIST: 28x28x1, 70,000장(Train: 55,000장, Validation: 5,000장, Test: 10,000장)

- CIFAR 10: 32x32x3, 65,000장(Train: 50,000장, Validation: 5,000장, Test: 10,000장)

※ 데이터의 directory만 지정해준다면 자신의 데이터를 쉽게 인가할 수 있습니다.

## 3. 환경
- OS: Window 10(Ubuntu 16.04 is possible)

- Graphic Card /RAM : 1080TI /32G

- Python 3.5

- Tensorflow-gpu version:  1.4.0rc2 

- OpenCV 3.4.1

## 4. 실험 및 결과 요약
