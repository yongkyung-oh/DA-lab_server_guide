DA-lab_server_guide v0.6
=============
Guideline for DA-lab server


## Server Address
[Server IP]
학교 교내 IP 접속 가능 (10.xxx.xxx.xxx)


## Sharedspace / Workspace  
Server 내 HDD (4TB) 작업환경 공유. 개인 환경 및 공유 환경. 
Workspace는 주기적으로 백업 계획 (~500GB)

`\\[Server IP]`

```
HDD (DA-lab)
|   Guide
|   Sharedspace
|   Workspace
|   Indiviudal Folder 
|   ...
```


## SSH program
SSH Shell program을 통해 서버 터미널에 접속. 추천 프로그램: putty+Xming / MobaXtermS

OpenSSH 대신에 지정 포트를 사용하여 접속. Remote host를 `[Server IP`로 입력하고, Port를 지정된 번호로 입력해야 접속 가능. 

![session](/session.PNG)

**참고자료**
* https://mobaxterm.mobatek.net/download.html
* https://m.blog.naver.com/PostView.nhn?blogId=pgh7092&logNo=221256069394&proxyReferer=https%3A%2F%2Fwww.google.com%2F


## 서버 상태 확인 
* 하드 용량 체크: `df -h`
* 메모리 체크: `free -m`
* GPU 체크: `nvidia-smi`


## Account 
설정된 계정을 사용하여 로그인 
비밀번호 설정 `passwd` 


## R-studio server 
웹브라우저를 통해 바로 접속 가능
`[Server IP]:8787`


## Python (Anaconda)
Anaconda / Jupyter notebook 기본 세팅으로 사용 

가상 환경을 사용하여 작업 `conda create -n [env name] [env packages]` 

예제: `yongkyung@da-server:/HDD$ conda create -n yk-tensorflow-gpu tensorflow-gpu`
![conda_example](/conda_example.PNG)

* 가상환경 확인: `conda env list`
* 가상환경 실행: `conda activate <env name>`
* 가상환경 종료: `conda deactivate`
* Jupyter Notebook 설치가 안된 경우: `conda install jupyter notebook`

예제: `(yk-tensorflow-gpu) yongkyung@da-server:/HDD$ conda install keras`
![conda_install_example](/conda_install_example.PNG)

**참고자료** 
* https://niceman.tistory.com/85
* https://niceman.tistory.com/86


## Jupyter Notebook 
anaconda를 사용하여 만든 가상환경에서 Jupyter notebook을 실행. 

#### 1. 가상환경 내에서 바로 실행
* 가상환경을 실행 `conda activate [env name]`
* Jupyter Notebook 설치 `conda install jupyter notebook`
* Jupyter Notebook 실행 `jupyter notebook`
* GUI를 불러와서 작업 수행

#### 2. Kernel 추가
* Jupyter Notebook에 Kernel 추가
`python -m ipykernel install --user --name [env name] --display-name "[display kenrel name]`
* Jupyter Notebook 실행 `jupyter notebook`
* Kernel 을 선택하여 notebook 작성 

#### 3. 외부 웹브라우저로 실행
* Jupyter Notebook 실행 시 IP와 Port를 지정하여 실행 
`jupyter notebook --ip [Server IP] --port xxxx`
* 개인 PC의 웹브라우저에서 해당 `[Server IP]:port` 를 사용하여 접속
* 터미널에서 Token 정보를 복사하여 서버에 로그인
* Kernel 을 선택하여 notebook 작성 


## 서버 활용 방법 
1. 기본 코드 작성 및 테스트는 개인 PC 에서 진행
2. 대용량 연산 및 작업 진행이 필요할때는 서버에서 작업
3. 백업이 필요한 코드,데이터,결과물의 경우 `Workspace`에 복사하여 수행 (매일 새벽 3시~5시에 동기화 수행 예정)


## Performance test
![Performance](/performance.PNG)


## Example: Install conda to deep-learning
#### Anaconda 설치
1. Shared Space로 이동 `cd /HDD/Saredspace`
2. 설치 파일 실행 `./Anaconda3-2018.12-Linux-x86_64.sh`
3. 환경변수 설정 `source ~/.bashrc `
4. 최신 버전으로 업데이트 `conda update conda`

#### 가상환경 생성
Keras 예제를 GPU로 수행
1. Keras와 Dependencies 를 설치하기 위한 가상 환경 세팅 `conda create -n [env name] python=3.6`
2. 설치된 가상환경 확인 `conda env list`
3. 가상환경을 실행 `conda activate [env name]`
4. 기본 패키지 설치 
    `conda install tensorflow-gpu`
    `conda install keras`
    `conda install matplotlib`
    `conda install jupyter notebook`
    혹은 `conda install tensorflow-gpu keras matplotlib jupyter notebook`

#### Jupyter Notebook 실행 및 접속
1. Jupyter notebook 실행 -> GUI 사용 `jupyter notebook`
2. IP 및 포트를 지정하여 실행 -> 토큰 인증 후 로컬 웹브라우저에서 사용 `jupyter notebook --ip=[Server IP] --port=xxxx`

#### 예제 코드 실행
* 현재 작업중인 가상환경 확인 코드
```{.python}
import os 
print(os.environ['CONDA_DEFAULT_ENV'])
```

* 시스템 확인 코드
```{.python}
import sys
import tensorflow as tf
import keras
print('Python version : ', sys.version)
print('TensorFlow version : ', tf.__version__)
print('Keras version : ', keras.__version__)
```

* 사용 가능한 디바이스 확인 코드
```{.python}
from tensorflow.python.client import device_lib
device_lib.list_local_devices()
```

* Hello World example using tensorflow
```{.python}
import tensorflow as tf

# Simple hello world using TensorFlow
hello = tf.constant('Hello, TensorFlow!')

# Start tf session
sess = tf.Session()

# Run show constant
print(sess.run(hello).decode)
```

#### Keras CNN 예제 파일 실행
`/HDD/Sharedspace/Keras CNN example.ipynb` 실행
![CNN](/cnn.jpg)

#### 가상환경 정리 및 삭제 
1. 설치된 가상환경 확인 `conda env list`
2. 가상환경 캐시 삭제 `conda clean -all` 혹은 `conda clean -a`
3. 가상환경 삭제 `conda remove -n [env name] --all`

## Example: Using Docker for deep-learning

## Contact
YongKyung Oh, ok19925@unist.ac.kr
