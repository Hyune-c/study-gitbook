# 문자열 생성으로 테스트

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

![](<../../../.gitbook/assets/image (13) (1).png>)

* `heap dump summary`
  * String이 다수를 차지하고 있음을 확인.

![](<../../../.gitbook/assets/image (9) (1).png>)

* `Objects - GC roots`
  * Retained가 압도적으로 높고 테스트를 위해 만든 클래스에서 발생함을 확인 가능.

### 기타

* 더 완벽한 로그를 위해서는 heap dump가 아닌 thread dump를 떠야 합니다.

{% embed url="https://www.baeldung.com/java-thread-dump" %}
