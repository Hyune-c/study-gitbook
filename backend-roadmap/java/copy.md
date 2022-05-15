# Copy

## Shallow Copy vs Deep Copy

### 얕은 복사 Shallow Copy

* 주소를 복사합니다.
* 한쪽의 수정이 이루어지면 다른 한 쪽에도 영향이 갑니다.

### 깊은 복사 Deep Copy

* 새로운 객체를 생성 합니다.
* 서로 간 영향이 없습니다.

## Java 에서 사용되는 Copy 메소드의 비교

| Method             | Primitive Type Copy | Non-Primitive Type Copy | Speed   |
| ------------------ | ------------------- | ----------------------- | ------- |
| System.arraycopy() | Deep                | Shallow                 | Fastest |
| Object.clone()     | Deep                | Shallow                 | Fast    |
| Arrays.copyOf()    | Deep                | Shallow                 | Fast    |
| Using for          | Depend on code      | Depend on code          | Slow    |

* Primitive Type 은 값 그 자체이기 때문에 Deep Copy 를 지원합니다.
* Non-Primitive Type 은 주소를 복사하며 Swallow Copy 를 지원합니다.

### clone()

clone() 은 shallow copy 를 지원합니다.\
deep copy 를 위해서는 Cloneable 를 구현하거나 해주거나 new 를 통해 deep copy 를 해주어야 합니다.

### 샘플 코드

* Cloneable 를 implements 하지 않은 사용자 정의 클래스
  * clone : shallow copy
  * forCopy : deep copy

| origin                                                                                                       | clone                                                                                                        | forCopy                                                                                                   |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| ![img](https://user-images.githubusercontent.com/55722186/74404681-869c9800-4e6e-11ea-95a9-004f243aae3b.png) | ![img](https://user-images.githubusercontent.com/55722186/74404745-b2b81900-4e6e-11ea-87c4-4e19f3f003f1.png) | ![](https://user-images.githubusercontent.com/55722186/74404762-bf3c7180-4e6e-11ea-853e-76dfe18a3724.png) |

```java
import java.util.Arrays;

public class test {
  public static class Temp {
    public int a;
    public Object obj;

    public Temp(int a) {
      this.a = a;
      this.obj = new Object();
    }

    public int getA() {
      return a;
    }
  }

  public static void main(String[] args) {
    Temp[] origin = new Temp[]{new Temp(1), new Temp(2), new Temp(280), new Temp(1500), new Temp(40000)};
    Temp[] arrayCopy = new Temp[5];

    System.arraycopy(origin, 0, arrayCopy, 0, 5);

    Temp[] clone = origin.clone();
    Temp[] copyOf = Arrays.copyOf(origin, 5);
    Temp[] forCopy = new Temp[5];
    
    for (int i = 0; i < origin.length; i++) {
      forCopy[i] = new Temp(origin[i].getA());
    }
  }
}
```
