





## AbstractAnnotationConfigDispatcherServletInitializer



在传统SpringMVC  项目开发中,  需要在web.xml中配置DispatcherServlet,还需要配置IOC容器监听器.



```xml
<!-- ioc容器-->
<context-param>
	<param-name>contextConfigLocation</param-name>
	<param-value>classpath:/applicationContext.xml</param-value>
</context-param>

<listener>
	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>

<!-- springmvc配置-->
<servlet>
		<servlet-name>SpringMVC</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>
				classpath:spring/spring-config-mvc.xml
			</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>SpringMVC</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
```


但如果你使用的是Servlet 3.1 规范,可以通过继承**AbstractAnnotationConfigDispatcherServletInitializer**来配置



```java
package com.ro.web.controller.order;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class MyWebInitializer extends AbstractAnnotationConfigDispatcherServletInitializer{

	@Override
	protected Class<?>[] getRootConfigClasses() {
		
		return new Class<?>[] {};
	}

	@Override
	protected Class<?>[] getServletConfigClasses() {
		
		return new Class<?>[] {WebConfig.class};
	}

	@Override
	protected String[] getServletMappings() {
		
		return new String[] {"*.do"};
	}

}

```

