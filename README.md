# [Colorization](https://github.com/richzhang/colorization)
이미지 흑백 > 컬러 

----------------------------

## 프로젝트 환경 구성

### mac OS Mojave (10.14.1)

### Install
#### [caffe](http://caffe.berkeleyvision.org/install_osx.html) 

- 해당 오픈소스 프로젝트 기반이 `caffe` 되어 있어서 설치 필요.
    > ### Dependencies ###
    > This code requires a working installation of [Caffe](http://caffe.berkeleyvision.org/) and basic Python libraries (numpy, pyplot, skimage, scipy). For guidelines and help with installation of Caffe, consult the [installation guide](http://caffe.berkeleyvision.org/) and [Caffe users group](https://groups.google.com/forum/#!forum/caffe-users).
- `Caffe` 를 설치 하기 위해서는 여러가지 tool 설치 필요
  - [참고 자료](https://github.com/koosyong/caffestudy/wiki/install_osx)
  - Homebrew
  - Anaconda 파이썬
  - CUDA 7
  - cuDNN
  - 기타 (파이썬 기본 라이브러리)
- [Caffe 설치 스크립트](https://gist.github.com/rizkyario/a09dcb10d652de7f7c56bb6ef6662384)
  - 설치 방법 모색 중에 간단한 방법을 발견하였습니다.

----------------------------

## 프로젝트 실행 (컴파일, 실행, 학습)

## 컴파일

### Caffe

```
$ git clone https://github.com/BVLC/caffe.git
$ cd caffe
$ mkdir build
$ cd build
$ cmake ..
$ make
```

### Colorization
```
$ git clone -b master --single-branch https://github.com/richzhang/colorization.git
$ cd colorization
$ ./models/fetch_release_models.sh
```

## 실행

- 흑백 > 컬러 실행 명령어
```
$ python ./colorize.py -img_in ./demo/imgs/ansel_adams.jpg -img_out ./out.png
```

## 학습 

(1) `caffemodel` 을 로드 하기 아래 스크립트 실행 (모델 : `models/init_v2.caffemodel`)
```
$ ./train/fetch_init_model.sh
```

(2) 수정된 `Caffe` 를 해당 폴더에 로드하기 위해 스크립트 실행
```
$ ./train/fetch_caffe.sh
```

(3) 이미지들을 저장해놓은 폴더(`/resources`)를 환경 변수로 설정 (`$PYTHONPATH`)

(4) 학습 실행 (사용할 GPU ID 필요)
```
$ ./train/train_model.sh [GPU_ID]
```

----------------------------

## 프로젝트 실험 결과 (실제 돌린 결과) 
### 예상 
![Teaser Image](http://richzhang.github.io/colorization/resources/images/teaser4.jpg)

### Legacy
- 더 이상 프로젝트 업데이트 하지 않음.

### 컴파일 실패
- 사용되는 라이브러리 버전 차이 존재.

