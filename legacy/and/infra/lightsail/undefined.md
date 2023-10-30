# 인스턴스 구성 예제

> 인스턴스 타입 선택, static ip, inbound 규칙은 잘 정리된 블로그로 대체 합니다.

{% embed url="https://jojoldu.tistory.com/512" %}

## 1. OS 세팅

{% hint style="info" %}
docker 를 사용한다면 lightsail container 가 더 좋은 선택 입니다.
{% endhint %}

```powershell
$ sudo apt-get update

### java 11
$ sudo apt install openjdk-11-jre-headless
$ sudo java -version


### docker
# 기본적인 패키지들이 최신 버전인지 확인하기
$ sudo apt-get update && upgrade

# apt가 HTTPS를 통해 repository를 이용하는 것을 허용할 수 있도록 해주는 패키지들 설치
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Docker 공식 GPG key 추가
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Docker repository 등록
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Docker 설치
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io

# 버전 확인
$ docker --version


### docker-compose
# docker-compose 바이너리 가져오기
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 링크 & 권한 추가
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
$ sudo chmod +x /usr/bin/docker-compose

# 버전 확인
$ sudo docker-compose -v
```

