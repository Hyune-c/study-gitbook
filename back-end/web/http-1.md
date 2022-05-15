# HTTP 그외

## Cookie vs Session

stateless 의 문제점을 보완하기 위한 방식이지만, 두 방식 모두 보안 위협이 존재하기에 OAuth, JWT 방식이 나왔습니다.

|          | Cookie            | Session |
| -------- | ----------------- | ------- |
| Stored   | Browser in Client | Server  |
| Security | 변조의 위험성           | 탈취의 위험성 |

## URI vs URL vs URN

URI 는 URL 과 URN 을 포함하는 슈퍼셋 입니다.

* URI (Uniform Resource Identifier) 는 통합 자원 식별자로 최근에는 URL 과 혼용해서 쓰이기도 합니다.
* URL (Uniform Resource Locator) 은 자원의 위치을 뜻합니다.
* URN (Uniform Resource Name) 은 위치와 상관없이 리소스의 이름값을 이용해서 접근합니다.

### URI 포맷

> URI

```
http://user:pass@www.example.jp:80/dir/index.htm?uid=1#ch1

scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]
{스키마}://{자격정보}@{서버주소}:{서버포트}/{계층적 파일 패스}?{쿼리 문자열}#{프래그먼트 식별자}
```

> URL

```
http://user:pass@www.example.jp:80/dir/index.htm
```
