## 가비지 컬렉션이란?
런타임 데이터 영역에 heap영역안에 new generation 이랑 old generation이 있다? 또 old generation 밑에 또 뭐있다 까지 적으면 완료


> 프로그램을 개발하다보면 사용하지 않는 메모리(Garbege)가 발생하는데 C나 C++ 같은 경우에 사용자가 직접 메모리를 정리해줘야한다.
하지만 JAVA의 경우 JVM이 자동적으로 가비지를 GC가 자동으로 정리해준다. JAVA에서 메모리는 Stack 영역과 Heap 영역에 할당된다. 
 

### Heap 영역 


### GC의 특징 stop the world / wheep>

#### stop the world 
> GC(가비지 컬렉션)을 실행하는 경우 JVM이 어플리케이션을 멈춘다. GC에 사용되는 스레드를 제외한 모든 스레드 또한 멈춘다.


### GC의 동작 방식 new old generation
