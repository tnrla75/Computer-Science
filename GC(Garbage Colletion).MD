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
> Major GC(Full GC) : Old Generation을 대상으로 하는 GC
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

# Major GC랑 Full GC랑 같음?? 설명마다 다름;
## GC의 종류
+ Serial GC
 > GC를 처리하는 쓰레드가 1개(싱글 쓰레드) 다른 GC에 비해 stop the world 시간이 길다. Mark Compact 알고리즘 사용

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkQ7kr%2FbtqwkWtXx4B%2F1FrNPofoHdrnBeuH4w2eVK%2Fimg.png)
+ Parallel GC
 > Young 영역의 GC를 멀티 쓰레드로 수행 Serial GC에 비해 stop the world 시간 감소

+ Parallel Old GC
 > parallel GC를 개선. Old 영역에서도 GC를 **멀티 쓰레드** 로 수행.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrzrFn%2Fbtqwl6pdr64%2FfZcmaHiORNRO4p8U2KTAq1%2Fimg.png)
+ Concurrent Mark Sweep(CMS) Collector 
 > stop-the-world 시간을 줄이기 위해 생김. compact 과정이 없음 . CPU리소스를 많이 사용, 메모리 파편화가 단점. 
 1. initial mark 단계에서 참조 상태인 객체를 짧은 시간에 Marking 함.
 2. 올스탑 없이 Concurrent Mark단계에서 참조상태 객체를 확인. 
 3. Remark단계에서 변경되거나 추가된 객체를 확인. 
 4. Concurrent Sweep 단계애서참조 되지 않는 객체를 정리.


그렇지만 CPU 소모량이 많고, 백그라운드 쓰레드는 정렬(compaction)을 하지 못하기 때문에 메모리 단편화가 생긴다. 그리고 CMS 백그라운드 쓰레드가 작업을 완료할 만큼 충분한 CPU 얻지 못하거나 힙에 메모리 단편화가 많으면 CMS는 Serial Collector로 동작한다. 즉 싱글 쓰레드를 사용해 전체 애플리케이션 쓰레드를 멈추고 Old Generation 영역을 정리한다. 그런 후 작업이 끝나면 다시 CMS 컬렉터로 동작한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbA5UD6%2Fbtqwl6pdvpX%2F8hPyoUpNyo7QvtB1tkVwmK%2Fimg.png)

+ G1 GC
 > Old , Young 영역의 개념이 없다. 하나 이상의 Resion 에서 객체를 복사해 다른 Reison 으로 이동 시키는 Region 개념을 도입. CMS Collector의 CPU 리소스 및 메모리 파편화 단점 해결
 > 
 > Heap에 전역적으로 Marking 하고 가장 많은 공간이 있는곳 부터 메모리 회수 진행
 > 
 > Eden, Survivor, Old 역할에 더해 Humongous와 Availabe/Unused라는 2가지 역할을 추가하였다. 
  + humonguous는 region 크기의 50%를 초과하는 객체를 저장하는 region을 의미한다
  + Availabe/Unused는 사용되지 않은 Region을 의미한다. 
 
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEUHoC%2Fbtqwk9zJiqP%2FOcKI4TxCvLAB2YHxZP9aY1%2Fimg.png)




# 추가
cms에서 쓰레드 언제 한개쓰고 언제 유휴상태 없는지 









