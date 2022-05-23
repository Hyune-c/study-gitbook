---
description: 20.01~20.06 기간에 한 프로젝트의 일부
---

# Side Project

## Airbnb

> 랜덤하면서 의미있는 숙소 정보를 가져오기 위한 방법

### 호텔 정보 & 이미지 URL 가져오기

```java
public static String ACCOMMODATION_BASE_URL = "http://data.jeonnam.go.kr/rest/namdolodgeist";
public static String IMAGE_BASE_URL = "https://source.unsplash.com/featured";
```

* 전라남도 숙박 정보 서비스 공공 API [공공 API Document](https://www.data.go.kr/data/15058702/openapi.do)
  * 공개된 API Document 에는 이미지 URL 이 존재했지만 실제로는 대부분 삭제된 이미지 였습니다.\
    <img src="../../.gitbook/assets/image (11).png" alt="" data-size="original">
* 그래서 랜덤한 이미지를 가져오기 위해 `unsplash` 사이트를 이용했습니다. [unsplash](https://source.unsplash.com/)
  * 이미지의 `refresh time` 이 2.5 초 정도이기에 `sleep(2800)` 을 통해 가져왔습니다.
* 총 1189 개 숙소 상세 정보, 4755 개 무작위 이미지 가져오기 완료
