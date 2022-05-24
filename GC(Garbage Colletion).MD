# 가비지 컬렉션이란?


> 프로그램을 개발하다보면 사용하지 않는 메모리(Garbege)가 발생하는데 C나 C++ 같은 경우에 사용자가 직접 메모리를 정리해줘야한다.
하지만 JAVA의 경우 JVM이 자동적으로 가비지를 GC가 자동으로 정리해주기 때문에 개발에만 집중 할 수 있다. 하지만 메모리가 언제 해제되는지 정확하게 알 수 없고 GC가 동작하는 동안에는 다른 동작을 멈추기 때문에 오버 헤드(특정 기능을 수행하는데 드는 간접적인 자원)가 발생한다

<br>


## GC의 특징 
   특징으로는 Stop and World 와 Mark And Sweep이 있다.
### stop the world
> GC(가비지 컬렉션)을 실행하는 경우 JVM이 어플리케이션을 멈춘다. GC에 사용되는 스레드를 제외한 모든 스레드 또한 멈춘다. 작업 완료 이후에 멈춘 어플리케이션은 다시 시작한다.

### Mark and Sweep
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGghBW%2FbtrvvDgIHRO%2FHxoX3w9skgah3xFVhfEgD0%2Fimg.png)

+ Mark : 먼저 사용되는 메모리와 사용되지 않는 메모리를 식별한다.
+ Sweep : 전 단계에서 사용되지 않음으로 식별된 메모리를 해제한다.
+ Compaction : 분산된 객체들을 Heap의 시작 주소로 모아 메모리가 할당된 부분과 그렇지 않은 부분으로 압축

<br> 



## GC의 대상
> 객체들은 실질적으로 Heap영역 에서 생성되고 Method, Stack 영역 등 Heap 영역에 생성된 객체의 주소만 참조하는 형식이다. 메소드가 끝나는 등으로 인해 Heap영역 에서 참조하고 있지 않는 객체가 발생하게 된다. 이런 객체들을 Unreachable 이라고 하며 GC가 제거해준다. 
> 
> Unreachable : 객체가 참조되고 있지 않은 상태, GC의 대상
> 
>Reachable : 객체가 참조되고 있는 상태

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbW5c5r%2FbtrvAb4nrdH%2FlYHuQZya8ECvEndRkQchjk%2Fimg.png)

<br> 

## Heap 영역의 구분과 GC 동작 과정
 >Eden, survival로 구분된 Young generation 과 Old Generation
 > 
 > Minor GC : Young Generation을 대상으로 하는 GC
 >
 > Major GC : Old Generation을 대상으로 하는 GC
> 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbti1oP%2FbtrvtcdoBC9%2FupBBOdB4mJF6tfyhL8GPbK%2Fimg.png)

1. 객체가 처음 생성되고 Eden 에 할당된다.
2. 시간이 지나 Eden 에 객체가 다 쌓이면 Minor GC가 발생
3. Minor GC가 발생하고 Reachable(객체가 참조된 상태) 객체들은 S0로 옮겨짐. Unreachable 객체는 Eden 영역이 클리어 될 때 메모리에서 사라짐
4. 다음 Minor GC 가 발생할 때 3번과 같은 과정이 발생한다. 기존에 S0에 있던 Reachable 객체들은 S1로 옮겨진다. 이때 age 값이 증가되어 옮겨진다. 살아남은 모든 객체들이 S1로 옮겨지면 S0와 Eden은 클리어 된다.
 > Survivor 간의 이동마다 age 값이 증가한다, Survivor 영역 중 하나는 반드시 비어있어야 한다.
5. 다음 Minor GC 가 발생하면 4번 과정이 반복된다. S1 이 차 있었으므로 S1의 객체들은 S0로 옮겨지고 Eden과 S1은 클리어 된다
6. Minor GC 를 반복해 살아남아 age 가 특정값 이상이 되면 Old Generation 으로 옮겨진다. 이 과정을 Promotion(진급) 이라 한다.
7. Promotion 이 반복되서 Old Generation 이 가득 차면 Major GC가 발생한다.

![](https://mirinae312.github.io/img/jvm_gc/JVMObjectLifecycle.png)







