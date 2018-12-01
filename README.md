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
```
$ git clone -b master --single-branch https://github.com/richzhang/colorization.git
$ cd colorization
$ ./models/fetch_release_models.sh
```

## 실행

- 테스트 명령어 예제 (컬러 > 흑백)
```
$ python ./colorize.py -img_in ./demo/imgs/ILSVRC2012_val_00041580.JPEG -img_out ./out.png
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

(4) Modify paths in data layers `./models/colorization_train_val_v2.prototxt` to locate where ImageNet LMDB files are on your machine. These should be BGR images, non-mean centered, in [0,255].

(5) Run `./train/train_model.sh [GPU_ID]`, where `[GPU_ID]` is the gpu you choose to specify. Notes about training:

(a) Training completes around 450k iterations. Training is done on mirrored and randomly cropped 176x176 resolution images, with mini-batch size 40.

(b) Snapshots every 1000 iterations will be saved in `./train/models/colornet_iter_[ITERNUMBER].caffemodel` and `./train/models/colornet_iter_[ITERNUMBER].solverstate`.

(c) If training is interupted, resume training by running `./train/train_resume.sh ./train/models/colornet_iter_[ITERNUMBER].solverstate [GPU_ID]`, where `[ITERNUMBER]` is the last snapshotted model.

(d) Check validation loss by running `./val_model.sh ./train/models/colornet_iter_[ITERNUMBER].caffemodel [GPU_ID] 1000`, where [ITERNUMBER] is the model you would like to validate. This runs the first 10k imagenet validation images at full 256x256 resolution through the model. Validation loss on `colorization_release_v2.caffemodel` is 7715.

(e) Check model outputs by running the IPython notebook demo. Replace the release model with your snapshotted model.

(f) To download reference pre-trained model, run `./models/fetch_release_models.sh`. This will load reference model `./models/colorization_release_v2.caffemodel`. This model used to generate results in the [ECCV 2016 camera ready](arxiv.org/pdf/1603.08511.pdf).

For completeness, this will also load model `./models/colorization_release_v2_norebal.caffemodel`, which is was trained without class rebalancing. This model will provide duller but "safer" colorizations. This will also load model `./models/colorization_release_v1.caffemodel`, which was used to generate the results in the [arXiv v1](arxiv.org/pdf/1603.08511v1.pdf) paper.

----------------------------

## 프로젝트 실험 결과 (실제 돌린 결과) 
