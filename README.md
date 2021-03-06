## 1. 프로젝트 개요

You can see the full description and English Version of this project:

https://github.com/MINGUKKANG/ENAS-Tensorflow

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

**사용방법**

1. 레포지토리에 있는 MNIST 데이터를 아래의 사진과 같이 압축해제 해줍니다.

   (개인 데이터를 쓰기위해서는 폴더 안에 이미지만 교체해주면 됨)

<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/unpack.PNG)

2. 아래의 코드를 자신의 상황에 맞게 재작성 해줍니다.

```
<main_controller_child_trainer.py , main_child_trainer.py>

DEFINE_integer("channel",재작성, "MNIST: 1, Cifar10: 3")
DEFINE_integer("img_size", 재작성, "enlarge image size")
DEFINE_integer("n_aug_img",재작성 , "if 2: num_img: 55000 -> aug_img: 110000, elif 1: False")

예)
DEFINE_integer("channel",1, "MNIST: 1, Cifar10: 3")
DEFINE_integer("img_size",32, "enlarge image size")
DEFINE_integer("n_aug_img",1, "if 2: num_img: 55000 -> aug_img: 110000, elif 1: False")
```
※ 네트워크를 찾아줄 때는 n_aug_img = 1, Child network를 학습시킬 때는 메모리 상태에 따라 선택하는 것을 권장합니다.

<br/>3. 끝난후에 Anaconda Prompt에서 해당 프로젝트 디렉토리에 진입한 다음 아래의 코드를 작성하여 코드를 실행시켜 줍니다.

```
python main_controller_child_trainer.py
```
<br/>4. 학습이 끝나 Child network의 후보인 child_arc_seq를 선택했다면 prompt에 다음과 같은 코드를 입력하여 실행시켜줍니다.
```
python main_child_trainer.py --child_fixed_arc "자신의 결과"

예)

Case of MNIST 

python main_child_trainer.py --child_fixed_arc "1 2 1 3 0 1 0 4 1 1 1 1 0 1 0 1 1 0 0 1 0 1 0 4 1 0 2 0 0 3 1 1 0 0 0 0 4 1 1 0"

Case of Cifar 10

python main_child_trainer.py --child_fixed_arc "1 0 1 1 1 1 0 0 1 1 0 0 0 3 0 3 1 3 1 1 1 1 0 3 0 3 0 3 1 3 0 1 1 3 0 2 0 3 1 0"
```

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

### 1. Micro search space에서 발견된 ENAS Cells

<main_controller_child_trainer.py>를 학습한 후에 얻은 child_arc_seq는 아래와 같습니다.

#### MNIST
```
"1 2 1 3 0 1 0 4 1 1 1 1 0 1 0 1 1 0 0 1 0 1 0 4 1 0 2 0 0 3 1 1 0 0 0 0 4 1 1 0"
```

<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/MNIST_convCell.png)

<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/MNIST_Reduction_cell.png)

#### CIFAR 10
```
"1 0 1 1 1 1 0 0 1 1 0 0 0 3 0 3 1 3 1 1 1 1 0 3 0 3 0 3 1 3 0 1 1 3 0 2 0 3 1 0"
```

<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/CIFAR10_Convolution_cell.png)

<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/CIFAR10_Reduction_cell.png)

### 2. 최종 Child Network의 구조

#### MNIST
<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/MNIST_Final.png)

#### CIFAR 10
<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/Final_structure_child_network.png)

### 3. Test Accuracy

```
MNIST
When n_aug_img is 2
Test Accuracy : 99.64% 
```

```
CIFAR 10(will be updated ASAP)
Test Accuracy : 
```

### 4. Schematic of Networks

#### 1. Controller Network
<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/Controller.PNG)

#### 2. Child Network
<br/>![사진](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/Child_Network_img.png)

### 5. Summary of Learning Mechanism
<main_child_controller_trainer.py>

```
1. Child Network를 1 Epoch만큼 학습시킨다.
2. Controller를 Adam Optimization을 이용하여 'FLAGS.controller_train_steps x FLAGS.controller_num_aggregate'번 학습시킨다.
3. 1과 2를 원하는 만큼 반복한다.(160Epoch)
4. 제안된 10개의 네트워크 중 가장 Validation Accuracy가 높은 모델을 선정한다.
```

<main_child_trainer.py>
```
1. 선택한 Child Network를 우리가 원하는 Epoch만큼 학습시켜준다.
(Momentum Optimization을 사용하였고, Cosine wave를 통해 lr를 주기적으로 변화시켜 주었다.)
```

## 5. Augmentation

### 1. Code

```python
def aug(image, idx):
    augmentation_dic = {0: enlarge(image, 1.2),
                        1: rotation(image),
                        2: random_bright_contrast(image),
                        3: Flip(image)}

    image = augmentation_dic[idx]
    return image
```

함수 enlarge, rotation, random_bright_contrast and Flip는 cv2를 이용해 작성되었습니다.

(※ MNIST데이터의 경우 Flip을 사용하지 않았음.) 

### 2. Images

#### MNIST
![사진9](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/MNIST_AUG.png)

#### CIFAR10
![사진9](https://github.com/MINGUKKANG/PNU_Termproject_ENAS/blob/master/images/Cifar10_AUG.png)

## 참조
**Paper: https://arxiv.org/abs/1802.03268**

**Autors' implementation: https://github.com/melodyguan/enas**

**Data Pipeline: https://github.com/MINGUKKANG/MNIST-Tensorflow-Code**

## License
All rights related to this code are reserved to the author of ENAS

(Hieu Pham, Melody Y. Guan, Barret Zoph, Quoc V. Le, Jeff Dean)
