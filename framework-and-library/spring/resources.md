# resources 경로에 있는 파일 가져오기

* Java 활용
  * java.lang.ClassLoader

```java
// public URL getResource(String name)
ClassLoader.getSystemResource("csv_s3_test.csv")
```



* Spring 활용
  * org.springframework.util.ResourceUtils

```java
// public static File getFile(String resourceLocation) throws FileNotFoundException
final File file = ResourceUtils.getFile("classpath:csv_s3_test.csv");
```
