DA-lab_server_guide v0.5
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


## 서버 상태 확인 
* 하드 용량 체크: `df -h`
* 메모리 체크: `free -m`
* GPU 체크: `nvidia -smi`


## Account 
설정된 계정을 사용하여 로그인 
비밀번호 설정 `passwd` 


## R-studio server 
웹브라우저를 통해 바로 접속 가능
`[Server IP]:8787`


## SSH program
SSH Shell program을 통해 서버 터미널에 접속. 추천 프로그램: putty+Xming / MobaXterm

**참고자료**
* https://m.blog.naver.com/PostView.nhn?blogId=pgh7092&logNo=221256069394&proxyReferer=https%3A%2F%2Fwww.google.com%2F


## Python (Anaconda)
Anaconda / Jupyter notebook 기본 세팅으로 사용 

가상 환경을 사용하여 작업 `conda create -n [env name] [env packages]` 
기본 설치 위치가 공동 작업 공간으로 되어있어서, 개별 가상 환경을 만들고 작업을 진행하는 것을 추천. 

예제: `yongkyung@da-server:/HDD$ conda create -n yk-tensorflow-gpu tensorflow-gpu`
![conda_example](/conda_example.PNG)

* 가상환경 확인: `conda env list`
* 가상환경 실행: `source activate <env name>`
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
* 가상환경을 실행 `source activate [env name]`
* Jupyter Notebook 실행 `jupyter notebook`
* GUI를 불러와서 작업 수행

#### 2. Kernel 추가
* Jupyter Notebook에 Kernel 추가
`python -m ipykernel install --user --name [virtualEnv] --display-name "[displayKenrelName]`
* Jupyter Notebook 실행 `jupyter notebook`
* Kernel 을 선택하여 notebook 작성 

#### 3. 외부 웹브라우저로 실행
* Jupyter Notebook 실행 시 IP와 Port를 지정하여 실행 
`jupyter notebook --ip [Server IP] --port xxxx`
* 개인 PC의 웹브라우저에서 해당 `[Server IP]:port` 를 사용하여 접속
* 터미널에서 Token 정보를 복사하여 서버에 로그인
* Kernel 을 선택하여 notebook 작성 

**참고**
현재 작업중인 가상환경 확인 코드
```
import os 
print(os.environ['CONDA_DEFAULT_ENV'])
```


## 서버 활용 방법 
1. 기본 코드 작성 및 테스트는 개인 PC 에서 진행
2. 대용량 연산 및 작업 진행이 필요할때는 서버에서 작업
3. 백업이 필요한 코드,데이터,결과물의 경우 `Workspace`에 복사하여 수행 (매주 일요일 새벽 3시~5시에 동기화 수행 예정)


## Contact
YongKyung Oh, ok19925@unist.ac.kr

