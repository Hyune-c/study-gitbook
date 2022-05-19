---
description: >-
  Amazon SDK 2.x 버전이 존재하지만 'Amazon S3 전송 관리자, Amazon SQS 클라이언트 측 버퍼링' 등 일부 기능이
  제한되어 있습니다.
---

# Amazon SDK 1.x with Spring

#### AmazonS3 Bean 설정

```java
@Configuration
@RequiredArgsConstructor
public class AmazonS3Beans {

	public static final Regions CLIENT_REGION = Regions.AP_NORTHEAST_2;

	@Value("${cloud.aws.credentials.accessKey}")
	private String accessKey;

	@Value("${cloud.aws.credentials.secretKey}")
	private String secretKey;

	@Bean
	public AmazonS3 amazonS3() {
		final BasicAWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
		return AmazonS3ClientBuilder.standard()
				.withCredentials(new AWSStaticCredentialsProvider(credentials))
				.withRegion(CLIENT_REGION)
				.build();
	}
}
```

* AWS 접근 방법을 하나로 통일시키기 위해 bean으로 설정할 수 있습니다.
  * 하나의 애플리케이션에서 복수 개의 AWS 접근 방법이 있다는 건 이상합니다.

#### PutObjectRequest 생성

```java
protected PutObjectRequest createRequest(final String objectKey, final File file, final CannedAccessControlList cannedAclHeader) {
	final PutObjectRequest request = new PutObjectRequest(bucketName, objectKey, file);
	request.setMetadata(ObjectMetadataType.getMetadata(file));
	request.withCannedAcl(cannedAclHeader);

	return request;
}
```

* object를 저장하기 위한 **PutObjectRequest** 생성을 위해 4가지가 필요합니다.
  * **bucketName** 대상 버킷 이름
  * **objectKey** 고유 식별자
  * **file** 대상 파일
  * **cannedAclHeader** 공개 범위
  * **metadata** 메타 데이터
    * **Content-Type** file이 아닌 stream으로 업로드 하는 경우 **application/octet-stream**가 지정됩니다.

{% embed url="https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.html" %}
metadata
{% endembed %}

#### PutObject - 객체 저장

```java
public PutObjectResult putObject(final PutObjectRequest request) {
	try {
		return amazonS3.putObject(request);
	} catch (final SdkClientException e) {
		log.error(e.getClass().getName(), e);
		throw EXCEPTION_AMAZON_S3_UPLOAD_FAIL.get();
	}
}
```

* **PutObjectResult**는 활용하지 않았습니다.
  * 기대한 api들이 없었습니다.
