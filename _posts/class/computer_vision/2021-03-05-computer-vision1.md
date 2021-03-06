---
layout: post
title: "computer vision 1"
subtitle: "기본 환경 설정"
categories: class
tags: computer_vision
comments: true
typora-copy-images-to: ..\..\assets\img\post
toc: true
---

인공지능을 포함한 모든 컴퓨터 관련 과정에서 배울 때 가장 먼저 하는 것이 환경설정과 같은 것을 먼저한다. 여기서는 python을 사용 하기 때문에 python과 각종 툴들을 설치하는 과정을 담도록 하겠다.

# 1. 개요

필요한 프로그램 및 라이브러리 설치

# 2. 설치

가상환경은 python의 버전이나 라이브러리의 버전을 새로설치하는 번거로움을 덜기위해서 설치한다. 여기에서도 보다 편리한 관리를 위하여 가상환경 anaconda를 설치 하겠다. anaconda를 설치하면 python은 자동으로 설치가 되니 따로 설치 하지 않아도 된다.

## 1) anaconda 설치

https://www.anaconda.com/download/ 이곳에 접속해서 다운을 받는다.

![image-20210305154504516](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305154504516.png)

저 부분을 클릭해서 들어간다

![image-20210305154616957](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305154616957.png)

다운로드 버튼을 클릭하고

![image-20210305154642114](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305154642114.png)

알맞은 버전을 다운 받는다. 그후 설치를 진행 하다보면

![image-20210305154819487](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305154819487.png)

이런 창이 나오는데 개인 컴퓨터면 위를 고르고 next를 누르면 된다. 계속 진행하다보면 다시 아래처럼 나오게 되는데

![image-20210305154942277](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305154942277.png)

여기서 윗 부분은 일반 cmd에서 사용 할꺼냐는 건데 anaconda말고 다른 인터프리터가 있을경우 충돌이 있으니 체크하면 안된다. 체크를 하지 않으면 anaconda에서만 사용할 수 있다. 아래 부분은 다른 IDE에서 파이썬 3.8을 기본으로 사용할 껀지 묻는 건데 체크해도 별 상관 없다.

![image-20210305160143284](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305160143284.png)

이제 anaconda prompt를 찾아서 실행해서 위처럼 나오면 설치가 끝난 것이다.

## 2) conda 개발 환경 구성

```python
# 아나콘다 버전확인
conda --version

# 아나콘다 업데이트
conda update conda

# 가상환경 생성
conda create --name <환경이름> python=3.8

# 설치된 가상환경 리스트 확인
conda info --envs

# 가상환경 활성화
conda activate <환경이름>

# 가상환경 비활성화
conda deactivate

# 가상환경 설치 package 확인
conda list --name <환경이름>

# 가상환경 package의 conda 이용 설치 (예:
tensorflow)
conda install -c anaconda tensorflow
conda install -c anaconda tensorflow-gpu

# 가상환경 package의 pip 이용 설치
(예: scipy)
pip install scipy

# 가상환경 삭제
conda remove --name <환경이름> --all

# openCV설치
pip install opencv-python
pip install opencv-contrib-python
```

위의 코드들이 conda 명령어인데 아까 확인한 conda prompt에서 사용하는 명령어 들이다. 자주 사용 할테니 알아두면 좋다.

### (1) 가상환경 생성

위의 명령어 중에서 `conda create --name <환경이름> python=3.8` 이 명령어를 사용하면 되는데

![image-20210305161104201](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161104201.png)

엔터를 누르면

![image-20210305161125816](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161125816.png)

이렇게 주르륵 나온다 y를 눌러서 마저 실행하자

조금 기다리면

![image-20210305161233879](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161233879.png)

이렇게 설치가 완료 되었다고 나오는데 위의 `conda info --envs`를 사용해서 확인해보면

![image-20210305161331694](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161331694.png)

이렇게 제대로 설치됨을 확인 할 수 있다.

### (2) 가상환경 실행

위의 `conda activate <환경이름>`를 이용하여 가상환경을 실행 할 수 있다.

![image-20210305161509592](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161509592.png)



가상 환경에서 나가고 싶다면 `conda deactivate`를 이용해서 밖으로 나올 수 있다.

![image-20210305161658431](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161658431.png)

### (3) 가상환경 구성

`conda list --name <환경이름>`를 이용하면 설치된 라이브러리들을 확인 할 수 있다.

![image-20210305161838125](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305161838125.png)



이제 각 가상환경에 필요한 라이브러리들을 설치해야하는데

numpy(계산하는 라이브러리), matplotlib(그래프 그리는 라이브러리) 이다

`conda install numpy`,`conda install matplotlib`을 설치 한다

### (4) 가상환경 삭제

만일 지우고 싶다면 `conda remove --name <환경이름> --all`를 이용해서 지울 수 있다.

## 3) IDE 설치 PyCharm

원래 VS code를 주로 사용하지만 한번 배워볼까 해서 사용해 보려 한다.

### (1) 설치

https://www.jetbrains.com/ko-kr/pycharm 이 주소로 들어가서

![image-20210305162736469](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305162736469.png)

다운로드 버튼을 누르고

![image-20210305162801813](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305162801813.png)

Community 버전을 다운 받는다.

그후 계속해서 설치를 하다보면

![image-20210305162959253](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305162959253.png)

이렇게 나오는데 무시하고 끝까지 설치하면 된다.

### (2) 기본 환경설정

![image-20210305163804429](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305163804429.png)

new project를 눌러서 프로젝트를 실행해 보자

![image-20210305164359736](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305164359736.png)

여기서 봐야 될것은 아래의 previously configued interpreter 인데

![image-20210305164834540](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305164834540.png)

이 부분의 끝의 버튼을 누르고 들어가면

![image-20210305164902457](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305164902457.png)

pycharm에 인터프리터를 추가할 수 있는 옵션이 나온다. 여기에서 conda로 들어가서

![image-20210305165001229](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305165001229.png)

아까 만든 가상환경을 누르고 create를 누르면 생성된다

파일을 만든 후에도 인터프리터를 변경할 수 있다.

[file] -> [setting]

![image-20210305204025204](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305204025204.png)

에 들어가면

![image-20210305204152174](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305204152174.png)

python interprreter가 있는데 여기에서 python interpreter옆의 톱니바퀴를 누르고 add를 누르면 아까와 똑같이 추가할 수 있는 창이 나온다.

![image-20210305204345458](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305204345458.png)



## 4) OpenCV 설치

Computer Vision에 관한 라이브러리 중 가장 중요한 것으로 설치를 해야 한다.

OpenCV 는 모듈이 2가지 있는데 그 2가지는 main modules와 extra modules가 있다. main modules 기본적인 기능을 모아놓은 모듈이고 extra modules는 최근에 새로나온 기능이나 인기가 없는 모듈 그리고 무료가 아닌 모듈, 하드웨어 의존성이 높은 모듈이 있다. 무료가 아닌 모듈은 상업적으로 이용하면 문제가 생기는 모듈을 뜻 한다.

### (1) 설치

이제 설치를 위해 아까 만들어 둔 가상환경으로 들어간다.

![image-20210305210750628](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305210750628.png)

`pip install opencv-python`과 `pip install opencv-contrib-python`을 이용해 설치 한다

왜 인지는 모르지만 conda설치가 지원하지 않는다고 한다

![image-20210305211213352](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305211213352.png)

### (2) 테스트

설치를 했으니 한번 확인을 해보자

```python
import cv2
print("Hello OpenCV", cv2.__version__)
img = cv2.imread('lena.bmp')
cv2.imshow('my_image', img)
cv2.waitKey()
cv2.destroyAllWindows()
```

아래의 코드는 그림 파일을 띄우는 코드인데 이 코드를 입력하고 실행한다.(파일이 있는 폴더와 같은 폴더 내에 해당그림이 있어야함)

![image-20210305212208722](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210305212208722.png)

정상적으로 작동이 된다. 아무키나 누르면 종료된다.

