---
title:  "Spring Interceptor"
date:   2019-02-24 23:58:00
categories: [Develop]
tags: [Spring, filter, interceptor]
---

# Spring Filter와 Interceptor의 차이

Spring **Filter**와 **Interceptor**을 보면 이 둘의 기능은 크게 차이가 없어 보인다. 하지만, 이 둘은 분명히 다른 것이고 더 알아보고 싶어 이 글을 통해 정리하게 되었다. 

## Filter와 Interceptor란?
![spring MVC request life cycle](/images/spring_mvc_request_life_cycle.png)

### Filter

- Filter는 DispatcherServlet으로 요청이 가기전, DispatcherServlet에서 응답을 하기전에 실행된다.
- 즉, 모든 요청, 응답에 대해 적용한다.


### Interceptor

- 컨트롤러에 들어오는 요청 HttpRequest와 컨트롤러가 응답하는 HttpResponse를 가로채는 역할을 한다.
- 스프링에서 관리되기 때문에 Spring내의 모든 객체에 접근이 가능하다.


### 차이점

1. 우선, Filter와 Inceptor는 **호출되는 시점**이 다르다.
Filter는 DispatcherServlet으로 요청이 가기전에 실행되는 반면, Interceptor는 DispatcherServlet에서 Controller로 가기전에 실행된다.

2. 케어할 수 있는 **영역**이 다르다.
Filter는 같은 웹 어플리케이션 내에서만 접근이 가능하며, Interceptor의 경우 Spring에서 관리되기 때문에 Spring내의 모든 객체에 접근이 가능하다.

3. 구현 방식
Filter는 Spring의 경우 Web.xml에 설정하여 구현이 가능하지만, Interceptor는 설정 이외에 **메서드 구현**이 필요하다.

### 결론
Filter와 Inteceptor는 각 상황에 맞게 활용되어야 한다. 과제로 메일서비스를 개발하면서, sitemesh를 적용하며 filter를 사용해보았고, session을 db와 redis로 관리하면서 interceptor를 통해 세션을 이용한 사용자의 권한을 인증하는 용도로 사용하였다. 정리를 하면서 이 둘의 차이는 알았지만, 아직 크게 어떤 상황에서 어떤 것이 적절한지에 대해 감이 잡히지는 않는다. 하지만, 이번 기회를 통해 차이가 있다는 것을 알게 되었고, 그러한 상황이 온다면 고민을 해보고 적절한 방법을 사용할 수 있도록 짚고 넘어가야 한다고 생각한다.



출처 : [https://meetup.toast.com/posts/151], [https://supawer0728.github.io/2018/04/04/spring-filter-interceptor/]
