# HTTP Request 추적하기 with HAR File

{% hint style="info" %}
HAR File, HTTP Archive File
{% endhint %}

#### Datadog 등의 모니터링 솔루션으로도 부족한 사용자의 시도를 분석 가능합니다.

* 재현 가능한 시도에 대해 크롬 베이스로 사용자 시도를 완벽히 분석 가능합니다.
* 불안정한 사용자 네트워크 환경도 분석할 수 있습니다.
* 서버 통신이 실패한 로그도 기록되기에 유실이 없습니다.

#### 비숙련자도 다룰 수 있을 정도로 쉽고 빠르고 간편합니다.

* 영업 직원은 물론이고 CS로 들어오는 일반 사용자 건에도 대응할 수 있습니다.

#### AWS에서도 이상 여부를 체크를 위해 사용되는 공식 요청 기록 중 하나입니다.

{% embed url="https://aws.amazon.com/ko/premiumsupport/knowledge-center/support-case-browser-har-file/" %}

## HAR 파일 만들기 by 사용자&#x20;

#### 1. 개발자 도구 실행 후 준비

* 웹 페이지에서 우클릭 후 팝업 메뉴에서 **검사** 버튼 클릭
* **Network** 탭 선택
* **Preserve log** 체크
* 기존 기록이 있는 경우 **모든 기록 Clear**

![](<../../../.gitbook/assets/image (16) (1).png>)

#### 2. 문제 상황 재현 후 HAR file 생성

* **Save All As HAR with Content** 또는 **Export HAR...** 를 통해 생

![](<../../../.gitbook/assets/image (16).png>)

#### 3. 생성된 HAR 파일을 전달

## HAR 파일 분석하기 by 개발자

#### 1. Chrome Extension 설치 & 실행

{% embed url="https://chrome.google.com/webstore/detail/http-archive-viewer/ebbdbdmhegaoooipfnjikefdpeoaidml/related?hl=ko" %}

![](<../../../.gitbook/assets/image (14).png>)

#### 2. HAR 파일을 드래그 앤 드랍

![](<../../../.gitbook/assets/image (13).png>)

## 참고 자료

{% embed url="https://devroach.tistory.com/125" %}
