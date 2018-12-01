# [Colorization](https://github.com/richzhang/colorization)
이미지 컬러 <-> 흑백 

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
- 설치 및 초기 셋팅
```
$ git clone -b master --single-branch https://github.com/richzhang/colorization.git
$ cd colorization
$ ./models/fetch_release_models.sh
```
- 테스트 예제 (컬러 > 흑백)
```
$ python ./colorize.py -img_in ./demo/imgs/ILSVRC2012_val_00041580.JPEG -img_out ./out.png
```

----------------------------

## 프로젝트 실험 결과 (실제 돌린 결과) 
