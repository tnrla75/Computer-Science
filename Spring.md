# 의존성 주입(Dependency Injection)

 * DI란 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴으로, 인터페이스를 사이에 둬서 클래스 레벨에서는
의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 해준다.

 * 의존성 주입은 필요한 객체를 직접 생성하는 것이 아닌 외부로 부터 필요한 객체를 받아서 사용하는 것이다.

# 제어의 역전(Inversion of Control

 * 스프링에서는 Application을 구성하는 Bean을 관리하기 위하여 IOC개념을 이용
Spring IOC Container가 객체를 관리함

 * Spring IOC Container가 주도권을 가져감으로써
객체의 관리, 의존관계의 결정 및 설정 등의 역할을 맡게된다.

 * 객체의 의존성을 개발자가 아닌 외부(IOC Container)에서 주입함으로써
객체간의 결합을 약하게 해주며 유지보수가 좋은 코드를 만들어준다.

# ORM(Object-Relational Mapping)

 * 객체와 DB의 테이블이 매핑을 이루는 것
 * ORM을 이용하면 SQL Query가 아닌 직관적인 코드(메서드)로서 데이터를 조작가능

# JPA(Java Persistent API)

 * ORM을 사용하기 위한 인터페이스를 모아둔 것
