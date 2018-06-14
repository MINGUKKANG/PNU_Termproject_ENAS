# Efficient Neural Architecture Search via parameter sharing.

1. 프로젝트 개요

**프로젝트 명**
Efficient Neural Architecture Search for Windows users.

**연구목적**
적절한 뉴럴네트워크를 디자인 하기위해서는 네트워크에 대한 많은 지식과 경험이 필요합니다.

하지만 ENAS를 사용하면 네트워크에 대한 지식없이도 높은 성능의 뉴럴네트워크를 손 쉽게 디자인 할 수 있는데 현재(2018.06.14) 공개된 ENAS는 다음과 같은 문제가 존재합니다.

네트워크에 데이터를 인가하려면 이미지 파일을 Pickle 파일로 변환한 다음 인가해주어야 해 비전공자들이 사용하기 어려운 따라서 저 
따라서 이번 프로젝트에서 저는 비전공자들이 사용하기 편하도록 데이터 파이프라인을 새로 구축하였고, Windows 유저들이 사용할 수 있도록 코드를 재구성 하였습니다. 나아가 Data를 손쉽게 Augmentation할 수 있도록하여 더욱 높은 성능의 네트워크를 얻을 수 있도록  
