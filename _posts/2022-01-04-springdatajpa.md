---
title: JPA적용
categories: 
  - Spring
tags:
  - Spring
last_modified_at: 2022-01-04T17:00:00+09:00
toc: true
---

# Spring Data Jpa 적용해보기

먼저 build.gradle에 아래와 같이 의존성 등록을 합니다.

```java

dependencies{
    implementation('org.springframework.boot:spring-boot-starter-data-jpa')
    implementation('com.h2database:h2')
}
```

spring-boot-starter-data-jpa

- 스프링 부트용 Spring Data Jpa추상화 라이브러리인데 스프링 부트 버전에 맞춰 자동으로 JPA관련 라이브러리들의 버전을 관리해준다.


H2

- 인메모리 관계형 데이터베이스이며, 메모리에서 실행되기 때문에 애플리케이션을 재시작할 때마다 초기화 된다는 점을 이용하여 테스트 용도로 많이 사용된다.


이제 JPA기능을 사용하여 도메인클래스를 작성할거다.


```java

package com.jojoldu.book.spring.domain.posts;
import com.jojoldu.book.spring.domain.BaseTimeEntity;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Getter
@NoArgsConstructor
@Entity
public class Posts extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(length = 500, nullable = false)
    private String title;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String content;

    private String author;

    //@Entity : 테이블과 링크될 클래스
    //@Id : 해당 테이블의 PK필드
    //@GeneratedValue : PK의 생성 규칙(스프링부트2.0에서는 GenerationType.IDENTITY옵션 추가시 auto_increment
    //@Column : 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용
    //Entity클래스에서는 Setter메소드 만들지 않는다!
    //해당 필드 값의 변경이 필요하면 메소드를 직접 추가
    @Builder
    public Posts(String title, String content, String author) {
        this.title = title;
        this.content = content;
        this.author = author;

    }
}


```

여기서 Posts클래스는 실제 DB의 테이블과 매칭될 클래스이며 보통 Entity클래스라고도 한다. 

JPA를 사용하면 DB데이터에 작업할 경우 실제 쿼리를 날리기보다 Entity클래스의 수정을 통해 작을을 한다.


**Entity**

- 테이블과 링크될 클래스임을 나타낸다.

**Id**

- 해당 테이블의 PK필드를 나타낸다.

**GeneratedValue**

- PK의 생성 규칙을 나타낸다.

- 스프링 부트 2.0에서는 GenerationType.IDENTITY옵션을 추가해 auto_increment가 된다.


다음과 같은 3개의 JPA 어노테이션 외에 어노테이션들은 롬복 라이브러리의 어노테이션이다.


**NoArgsConstructor**

- 기본 생성자 자동 추가( public Posts() {} 와 같은 효과)


**Getter**

- 클래스 내 모든 필드의 Getter메소드를 자동생성


**Builder**

- 해당 클래스의 빌더 패턴 클래스 생성


이 Posts클래스를 보면 Getter메소드는 있는데 Setter메소드는 없는 것을 볼 수 있다.

Getter, Setter메소드를 무작정 생성하면 해당 클래스의 인스턴스 값들이 언제 어디서 변해야 하는지 코드상으로 명확하게 구분할 수 없어, 차후 기능 변경 시 복잡해진다.

그래서 Entity클래스에서는 절대 Setter메소드를 만들지 않는다.


**잘못된 예**

```java

public class Order{
    public void setStatus(boolean status){
        this.status = status
    }
}

public void 주문서비스의_취소이벤트(){
    order.setStatus(false);
}
```


**올바른 예**


```java

public class Order{
    public void cancelOrder() {
        this.status = false;
    }
}

public void 주문서비스의_취소이벤트() {
    order.cancelOrder();
}


```

 위 코드를 비교하여 보면 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야한다.



 Setter가 없는 상황에서 DB에 값을 채우는 방법은 기본적으로 생성자를 통해 최종값을 채운 후 DB에 삽입하는 것이고, 값 변경이 필요한 경우 해당 이벤트에 맞는 public메소드를 호출하여 변경한다.


 하지만 저번에 봤던 이동욱 저자의 스프링부트와 aws로 혼자 구현하는 웹 서비스책을 보고 builder클래스를 사용해봤다.

 생성자나 빌더나 생성 시점에 값을 채워주는 역할은 똑같지만 생성자의 경우 지금 채워야 할 필드가 무엇인지 명확히 지정할 수 없다.  간단한 코드를 보면 더 쉽게 이해할 수 있을 것 같다.



**생성자**

 ```java

 public Example(String a, String b){
     this.a = a;
     this.b = b;
 }

 ```

**빌더**

```java

public Example(String a, String b){
    Example.builder()
           .a(a)
           .b(b)
           .build();
}

```