# 임의의 문자열 생성

```java
// -Xmx512m -Xms512m

@Slf4j
@RestController
public class AddStringController {

	@GetMapping("/add-string/run")
	public void run(@RequestParam final Integer millis) throws InterruptedException {
		final Thread thread = new Thread(new AddStringRunnable());
		thread.start();

		Thread.sleep(millis);
		thread.interrupt();
	}

	public static class AddStringRunnable implements Runnable {

		private final List<String> list = new ArrayList<>();

		public void run() {
			log.info("### AddString start");
			final byte[] array = new byte[7];
			try {
				while (true) {
					new Random().nextBytes(array);
					list.add(new String(array, StandardCharsets.UTF_8));
					Thread.sleep(0);
				}
			} catch (final InterruptedException e) {
				log.info("### AddString interrupt");
			}
		}
	}
}
```

![](<../../../.gitbook/assets/image (11).png>)

* OOM 발생

![](<../../../.gitbook/assets/image (13).png>)

* `heap dump summary`
  * String이 다수를 차지하고 있음을 확인.

![](<../../../.gitbook/assets/image (9) (1).png>)

* `Objects - GC roots`
  * Retained가 압도적으로 높고 테스트를 위해 만든 클래스라는 것을 확인 완료.

### 남은 의문

* `AddStringRunnable`의 `Thread.sleep(0);`를 0보다 큰 값으로 주면 정상 작동된다.
  * 어떤 차이가 있는거지?
* `GC roots`를 통해 어떤 클래스까지는 추적이 되지만, 정확히 어떤 메서드나 라인에서 발생했는지 추적하고 싶다.
  * error trace처럼 자세하면 좋겠다.
