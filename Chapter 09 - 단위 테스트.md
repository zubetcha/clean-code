# Chapter 09 - 단위 테스트

## TDD 세 가지 법칙

1. 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
2. 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3. 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

##

- 테스트 코드도 실제 코드와 마찬가지로 깨끗하게 유지하기
- 테스트 케이스 X -> 모든 변경은 잠정적인 버그
- 가독성
- 실제 코드만큼 효율적일 필요는 X
- 함수 하나 당 하나의 assert...
- 테스트 슈트는 순수함수..?

## BUILD-OPERATE_CHECK 패턴

<p align="center">
  <img src="https://miro.medium.com/v2/resize:fit:1260/format:webp/1*YslDrfj6TUWlQvaUoC3xXQ.jpeg" alt="build-operate-check-pattenr" width="70%" />
</p>

- BUILD: 테스트 자료 구성
- OPERATE: 테스트 자료 조작
- CHECK: 올바른 결과가 나오는지 확인

[참고](https://medium.com/swlh/usual-production-patterns-applied-to-integration-tests-50a941f0b04a)

## TEMPLATE-METHOD 패턴

- 객제지향 디자인 패턴 중 하나로, 기능의 뼈대(템플릿)과 실제 구현을 분리하는 패턴
- 상속을 통해 기능을 확장할 때 사용
- 변하지 않는 기능은 슈퍼 클래스, 자주 변경되고 확장해야 하는 기능은 하위 클래스

```java
public abstract class AbstractClass {

    protected abstract void hook1();

    protected abstract void hook2();

    public void templateMethod() {
        hook1();
        hook2();
    }

}

public class ConcreteClass extends AbstractClass {

    @Override
    protected void hook1() {
        System.out.println("ABSTRACT hook1 implementation");
    }

    @Override
    protected void hook2() {
        System.out.println("ABSTRACT hook2 implementation");
    }

}

public class TemplateMethodPatternClient {
    public static void main(String[] args) {
        AbstractClass abstractClass = new ConcreteClass();
        abstractClass.templateMethod();
    }
}
```

[출처](https://yaboong.github.io/design-pattern/2018/09/27/template-method-pattern/)

## F.I.R.S.T

- Fast: 빠르게
- Independent: 독립적으로
  - 각 테스트는 서로를 의존하지 않도록 작성
  - 순서도 상관이 없어야 함
- Repeatable: 어떠한 환경에서도 반복 가능하게
- Self-Validating: 자가 검증
  - 불린을 반환하여 스스로 성공인지, 실패인지 알 수 있도록
- Timely: 적시에
