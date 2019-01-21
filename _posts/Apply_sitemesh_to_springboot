---
title:  "스프링 부트에 sitemesh 3 적용하기"
date:   2019-01-21 21:58:00
categories: [Develop]
tags: [Spring | sitemesh]
---

스프링 부트(프로젝트 생성시, spring starter project)에서 sitemesh를 적용하는 방법은 다른 사람들이 올려놓은 적용방법과 많이 달랐다.
여기저기 찾으면서 내가 필요한 정보가 조금씩 부족했고, 시행착오를 토대로 적용법을 작성해보았다.

## 1. SiteMesh 설치 : http://wiki.sitemesh.org/wiki/display/sitemesh3/Getting+Started+with+SiteMesh+3

위 주소에서 sitemesh3을 다운받는다.
압축 파일을 풀고, WEB-INF/lib에 이 폴더를 저장한다.
WEB-INF/lib폴더가 없으면 새로 만든다.


## 2. pom.xml에 dependency추가하기.

```ruby
<dependency>
			<groupId> org.sitemesh</groupId>
			<artifactId> sitemesh </artifactId>
			<version> 3.0.0</version> 
</dependency>
```

이 부분에서 가장 고생했던건, version태그에 3.0으로 써서 WEB-INF/lib에 있는 폴더를 찾지 못했다.
꼭, 3.x.x 형식으로 써야한다.


## 3. src/main/java/....에 해당하는 경로에 클래스 파일을 추가한다
나는 src/main/java/.../deco패키지를 만들었고 (...는 본인이 쓰는 경로)
ServletFilterConfig.java와 SitemeshFilter.java 클래스 파일을 추가했다.

1. ServletFilterConfig.java
```ruby
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ServletFilterConfig {
		
	@Bean
	public FilterRegistrationBean siteMeshFilter() {
		FilterRegistrationBean filter = new FilterRegistrationBean();
		filter.setFilter(new SitemeshFilter());	
		return filter;
		
	}	
}
```
-> filter.setFilter(new SitemeshFilter())에서 SitemeshFilter는 아래 클래스 파일에서 정의한 클래스 이름으로 사용한다. 

2. SitemeshFilter.java
```ruby
package com.nhnent.wind.web.bom.deco;

import org.sitemesh.builder.SiteMeshFilterBuilder;
import org.sitemesh.config.ConfigurableSiteMeshFilter;

public class SitemeshFilter extends ConfigurableSiteMeshFilter{
	
	@Override
	protected void applyCustomConfiguration(SiteMeshFilterBuilder builder) {
		builder.addDecoratorPath("/*", "/WEB-INF/decorator/layout.jsp");
	}
}

```
-> builder.addDecoratorPath에서 첫번째 인수는 decorator을 적용할 경로이고, 두번째 인자는 가져다 쓸 decorator(layout)파일의 경로를 쓰면 된다.

## 4.decorator파일 생성

decorator 즉, layout으로 설정할 파일을 추가한다.
경로는 src/main/webapp/WEB-INF/...경로에 알맞게 파일을 추가한다. 나는 layout.jsp로 추가했다.

```ruby
<%@ page language="java" contentType="text/html; charset=EUC-KR"
	pageEncoding="EUC-KR"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title><sitemesh:write property='title' /></title>
<sitemesh:write property='head' />
</head>
<body>

	<sitemesh:write property='body' />

</body>
</html>

```

-> 이러한 형태로 decorator을 제외한 페이지들에서는 head, title, body부분만 작성하고, 그 외의 부분들은 layout이 적용되게 된다.




출처 : [https://pumdaf.tistory.com/entry/Spring-spring-boot-sitemesh3]
