# 제어의 역전(Inversion of Control

 * 스프링에서는 Application을 구성하는 Bean을 관리하기 위하여 IOC개념을 이용
Spring IOC Container가 객체를 관리함

 * Spring IOC Container가 주도권을 가져감으로써
객체의 관리, 의존관계의 결정 및 설정 등의 역할을 맡게된다.

 * 객체의 의존성을 개발자가 아닌 외부(IOC Container)에서 주입함으로써
객체간의 결합을 약하게 해주며 유지보수가 좋은 코드를 만들어준다.
