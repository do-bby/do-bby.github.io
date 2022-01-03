---
title: SpringBoot
categories:
- blogging
last_modified_at: 2022-01-03T16:00:00+09:00
toc: true
---

## SpringBoot란?

![스프링부트](https://user-images.githubusercontent.com/58400107/147909255-2cfbeb7b-73a5-4671-880c-d6915d0d8049.PNG)

##### **SpringBoot는 Java를 기반으로 한 웹 어플리케이션 프레임워크이다.** SpringBoot가 등장하기 전 Spring 프레임 워크가 먼저 등장했는데 Spring의 초기 환경 설정시 시간적인 문제를 해결하고자 등장한 프레임워크가 SpringBoot이다.
##### **SpringBoot는 Maven이나 Gradle의 dependency에 Starter라이브러리만 작성한다면 초기 세팅에 필요한 라이브러리들을 모두 세팅하여 초기 환경 설정을 간소화 시킬 수 있게 되었다.**
##### SpringBoot의 두번째 특징은 **Tomcat과 같은 내장 서버가 존재한다는 것이다.** Spring 프레임워크의 경우 Tomcat을 직접 설치해 프로젝트 내에서 서버를 설정해주고, 버전관리도 함께 해주어야 했다. 하지만 SpringBoot는 Tomcat내장 서버가 존재하여 설치, 버전관리를 신경쓰지 않아도 된다.
##### 마지막 특징으로 Spring의 경우 servlet-context, root-context와 같은 xml 파일을 직접 작성해서 web과 관련된 설정, Spring 프로젝트 내 객체 의존성을 관리 해야 했지만, **SpringBoot는 자동으로 의존성 관리가 가능하다.**

## Maven과 Gradle

![메이븐 그레들](https://user-images.githubusercontent.com/58400107/147909280-b61a32d1-1bb5-431a-b344-f9e453e5a13e.PNG)

##### 초기 개발 환경 설정 시 Maven의 pom.xml이나 Gradle의 build.gradle파일을 통해 프로젝트를 관리 할 수 있는데 Maven은 자바용 프로젝트 관리 툴이기 떄문에 자바에서만 사용 가능하다. 하지만 Gradle은 Java외에도 C++, Python 등 다양한 언어를 지원한다는 차이가 있다. 