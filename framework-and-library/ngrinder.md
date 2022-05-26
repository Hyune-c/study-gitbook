# nGrinder

![](<../.gitbook/assets/image (3) (1) (1).png>)

{% embed url="https://github.com/naver/ngrinder" %}

## 1. Controller 세팅

```shell
// 1. controller 다운로드
> wget https://github.com/naver/ngrinder/releases/download/ngrinder-3.5.5-p1-20210531/ngrinder-controller-3.5.5-p1.war

// 2. controller 기동 
> java -jar ngrinder-controller-3.5.5-p1.war --port 7070  
```

* [http://localhost:7070/login](http://localhost:7070/login)&#x20;
  * 초기 계정 정보 admin/admin

## 2. Agent 세팅

![admin > 에이전트 다운로드](<../.gitbook/assets/image (10) (1) (1).png>)

```shell
// 1. agent 다운로드 후 압축 해제
> tar -xvf ngrinder-agent-3.5.5-p1-localhost.tar 

// 2. agent 기동 
> ./run_agent.sh        // 일반 기동 
> ./run_agent_bg.sh    // 백그라운드에서 기동 
```

![admin > 에이전트 관리](<../.gitbook/assets/image (1) (1).png>)

* agent가 정상적으로 기동되고 승인된 것을 확인할 수 있습니다. (진한 파란색 토큰)

{% hint style="info" %}
만약 클라우드 환경에 설치한다면 설정을 수정해줘야 합니다.
{% endhint %}

```shell
> vi __agent.conf

common.start_mode=agent
agent.controller_host=localhost // host 정보 변경
agent.controller_port=16001
agent.region=NONE
```

## 3. 테스트 준비 & 실행

### 스크립트 생성

![스크립트 > 만들기 > 스크립트 만들기](<../.gitbook/assets/image (6) (1) (1).png>)

* **google.com** 으로 샘플 스크립트를 만듭니다.

### 성능 테스트

![성능 테스트 > 테스트 생성](<../.gitbook/assets/image (9) (1).png>)

* **저장 후 시작**을 누르면 바로 실행 됩니다.
* **Ramp-Up**을 활용하면 점진적으로 트래픽을 늘릴 수 있습니다.

![테스트 결과](<../.gitbook/assets/image (6) (1).png>)

## 기타

* script 실행 중 Unsupported 에러가 발생하면 java version을 확인해봅시다.
  * 저는 java 17 버전을 쓰고 있었기에 에러가 발생했고, 11로 교체 후 정상 작동하였습니다.&#x20;

```
General error during conversion: Unsupported class file major version 61
```
