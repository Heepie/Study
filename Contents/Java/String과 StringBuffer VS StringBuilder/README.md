# String과 StringBuffer VS StringBuilder

## String과 메모리</br>
String 객체는 한 번 생성될 때 메모리 공간이 고정되었다. 그리고 '+'나 'concat' 메소드를 사용해 문자열이 길어지면서 </br>
1) 의도 하지 않는 메모리 침범</br>
2) 제 3의 새로운 객체 생성 (∵ 할당된 메모리를 변경할 수 없으므로)</br>
이러한 문제가 있었다.</br></br>
그래서 JDK 1.5 버전 이후 String은 모두 StringBuilder로 컴파일러에서 자동으로 처리한다.
</br></br>

## 동기화란?
동기화(synchronization)는 데이터를 같게(=) 하는 것을 의미한다. 다르게 생각해보면 **"데이터 일치를 위해 A가 데이터를 수정 중에는 B는 데이터를 수정을 할 수 없다"**는 것을 의미한다.</br></br>

## StringBuffer VS StringBuilder
StringBuffer와 StringBuilder의 가장 큰 차이는 **"동기화 지원 여부"** 이다.</br></br>
StringBuffer, StringBuilder는 같은 메소드와 인터페이스를 상속 구현하지만 오버라이딩 메소드를 확인하면 StringBuffer는 "synchronized" 키워드로 동기화를 지원하지만 StringBuilder는 동기화를 지원하지 않는다.</br>

- StringBuffer
```java
public final class StringBuffer
    extends AbstractStringBuilder
    implements java.io.Serializable, CharSequence
{
...
    @Override
    public synchronized StringBuffer append(Object obj) {
        toStringCache = null;
        super.append(String.valueOf(obj));
        return this;
    }
...
}
```

- StringBuilder
```java
public final class StringBuilder
    extends AbstractStringBuilder
    implements java.io.Serializable, CharSequence
{
...
    @Override
    public StringBuilder append(Object obj) {
        return append(String.valueOf(obj));
    }
...
}
```

그래서 동시에 처리 가능한 StringBuilder는 동시에 처리 가능하지 않은 StringBuffer보다 상대적으로 속도가 빠르다. (∵ 동기화를 지원하지 않기 때문에 A, B, C 등 많은 클라이언트가 동시에 접속해 수정 가능)
