---
layout: post
title:  "Eclipse로 Spring 개발하기"
date:   2022-02-20 18:21:00 +0900
categories: eclipse spring web
---

# Ecipse build error

### org.apache.log4j.Logger cannot be resolved to a type 오류
```
@Log4j
@Service
@AllArgsConstructor
public class BoardServiceImpl implements BoardService {
```
@Log4j 선언부에서 발생한 에러임. 해결 방법은 아래 scope runtime 선언을 제거하면 해결됨.
```
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.15</version>
    <scope>runtime</scope>
</dependency>
```

### Tomcat Web Modules 패스 설정하기
tomcat이 등록된 Servers탭에서 tomcat 항목을 더블 클릭하면 아래 Web Modules 항목이 나타난다. Edit를 누르고 Path 항목의 /Controller를 /으로 변경한다.
![Web Modules 설정](/assets/img/2022-02-21_20.27.47_eclipse_web_module.png)

### web-app xsd 에러
```
There are '37' errors in 'https://java.sun.com/xml/ns/javaee/
 jsp_2_1.xsd'.
 ```
xsi:schemaLocation 항목을 세미콜론(;)으로 구분하면 해결된다.
```
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee; https://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">
```
[출처:https://code-hyoon.tistory.com/14](https://code-hyoon.tistory.com/14)
