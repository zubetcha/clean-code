# Chapter 08 - 경계

## ADAPTOR 패턴

- 클래스와 인터페이스를 사용자가 기대하는 다른 인터페이스로 변환하는 패턴
- 호환성이 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들이 함께 작동하도록 해줌
- 간에 붙었다 쓸개에 붙었다..
- 변환하는 기존 구조와 새 구조의 메소드 이름은 같을 수록 좋음

```java
/**
 * Java code sample
 */

/* the client class should instantiate adapter objects */
/* by using a reference of this type */
interface Stack<T>
{
  void push (T o);
  T pop ();
  T top ();
}

/* DoubleLinkedList is the adaptee class */
class DList<T>
{
  public void insert (DNode pos, T o) { ... }
  public void remove (DNode pos) { ... }

  public void insertHead (T o) { ... }
  public void insertTail (T o) { ... }

  public T removeHead () { ... }
  public T removeTail () { ... }

  public T getHead () { ... }
  public T getTail () { ... }
}

/* Adapt DList class to Stack interface is the adapter class */
class DListImpStack<T> extends DList<T> implements Stack<T>
{
  public void push (T o) {
    insertTail (o);
  }

  public T pop () {
    return removeTail ();
  }

  public T top () {
    return getTail ();
  }
}
```

```javascript
var senateSystem = new SenateSystem(currentAdapter); // 현재 시스템
var senateSystem = new SenateSystem(newAdapter); // 신규 시스템

var SenateSystem = (function () {
  function SenateSystem(adapter) {
    this.adapter = adapter;
  }
  SenateSystem.prototype.vote = function () {
    this.adapter.vote();
  };
  return SenateSystem;
})();

var currentAdapter = {
  vote: function () {
    console.log("현 황제를 계속 지지합니다");
  },
};

var rufusAdapter = {
  vote: function () {
    console.log("루푸스를 황제로 추대합시다");
  },
};

senateSystem = new SenateSystem(currentAdapter);
senateSystem.vote(); // 현 황제를 계속 지지합니다.
senateSystem = new SenateSystem(rufusAdapter);
senateSystem.vote(); // 루푸스를 황제로 추대합시다.

var galbaAdapter = {
  vote: function () {
    console.log("갈바를 황제로 추대합시다");
  },
};

senateSystem = new SenateSystem(galbaAdapter);
senateSystem.vote(); // 갈바를 황제로 추대합시다.
```

[참고](https://www.zerocho.com/category/JavaScript/post/57babe9f5abe0c17006fe230)
