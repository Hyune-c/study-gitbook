# 파일 조작하기

### resources 경로의 파일 접근

```java
// java.lang
// public URL getResource(String name)
ClassLoader.getSystemResource("csv_s3_test.csv")

// org.springframework.util
// public static File getFile(String resourceLocation) throws FileNotFoundException
final File file = ResourceUtils.getFile("classpath:csv_s3_test.csv");
```

### 파일 확장자 가져오기

```java
// org.springframework.util
// public static String getFilenameExtension(@Nullable String path)
return find(StringUtils.getFilenameExtension(file.getName()));
```
