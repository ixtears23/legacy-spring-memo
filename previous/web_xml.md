# XML 정리

 > **스프링 컨텍스트** 는 **루트**와 **자식컨텍스트**로 나눠진다.  
 > 전통적인 XML 기반 접근 방식  
 > 웹 응용 프로그램을 작성하는 대부분의 Spring 사용자는 **Spring(DispatcherServlet)을 등록**해야한다.  
 > WEB-INF/web.xml  

    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	id="WebApp_ID" version="3.0">
	<display-name>osp_sdn</display-name>
	<filter>
		<filter-name>encodingFilter</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>utf-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encodingFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
	<filter>
		<filter-name>HTMLTagFilter</filter-name>
		<filter-class>egovframework.rte.ptl.mvc.filter.HTMLTagFilter</filter-class>
	</filter>
	<filter-mapping>
		<filter-name>HTMLTagFilter</filter-name>
		<url-pattern>*.do</url-pattern>
	</filter-mapping>
	<filter-mapping>
		<filter-name>HTMLTagFilter</filter-name>
		<url-pattern>*.json</url-pattern>
	</filter-mapping>
	<!-- <filter> <filter-name>springSecurityFilterChain</filter-name> <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class> 
		</filter> <filter-mapping> <filter-name>springSecurityFilterChain</filter-name> 
		<url-pattern>/*</url-pattern> </filter-mapping> <listener> <listener-class>org.springframework.security.web.session.HttpSessionEventPublisher</listener-class> 
		</listener> -->
	<filter>
		<filter-name>AuthenticationFilter</filter-name>
		<filter-class>osp.sdn.common.web.filter.AuthenticationFilter</filter-class>
	</filter>
	<filter-mapping>
		<filter-name>AuthenticationFilter</filter-name>
		<url-pattern>*.do</url-pattern>
	</filter-mapping>
	<filter-mapping>
		<filter-name>AuthenticationFilter</filter-name>
		<url-pattern>*.json</url-pattern>
	</filter-mapping>

	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath*:egovframework/spring/context-*.xml</param-value>
	</context-param>
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
	<servlet>
		<servlet-name>action</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>/WEB-INF/config/egovframework/springmvc/dispatcher-servlet.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>action</servlet-name>
		<url-pattern>*.do</url-pattern>
	</servlet-mapping>
	<servlet-mapping>
		<servlet-name>action</servlet-name>
		<url-pattern>*.json</url-pattern>
	</servlet-mapping>
	<mime-mapping>
		<extension>eot</extension>
		<mime-type>application/vnd.ms-fontobject</mime-type>
	</mime-mapping>
	<mime-mapping>
		<extension>otf</extension>
		<mime-type>font/opentype</mime-type>
	</mime-mapping>
	<mime-mapping>
		<extension>ttf</extension>
		<mime-type>font/truetype</mime-type>
	</mime-mapping>
	<mime-mapping>
		<extension>woff</extension>
		<mime-type>application/font-woff</mime-type>
	</mime-mapping>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.do</welcome-file>
		<welcome-file>index.jsp</welcome-file>
	</welcome-file-list>
	<login-config>
		<auth-method>BASIC</auth-method>
	</login-config>
	<session-config>
		<session-timeout>60</session-timeout><!-- 분 -->
	</session-config>
	<error-page>
		<exception-type>java.lang.Throwable</exception-type>
		<location>/common/error.jsp</location>
	</error-page>
	<error-page>
		<error-code>404</error-code>
		<location>/common/error.jsp</location>
	</error-page>
	<error-page>
		<error-code>500</error-code>
		<location>/common/error.jsp</location>
	</error-page>
    </web-app>
    

# ContextLoaderListener
계층별로 나눈 xml 설정파일이 있다고 가정할 때 web.xml에서 모두 load되도록 등록할 때 사용.
서블릿이전에 서블릿 초기화하는 용도록 쓰이며 **contextConfigLocation** 라는 파라미터를 써서, 
Context Loader가 load할 xml설정파일을 등록할 수 있다.

 > web.xml에 `<context-param>` 문장이 빠지게 되면 default로,
 > /WEB-INF/applicationContext.xml (spring 설정파일) 을 쓰게 된다.
 > 경로를 잘못 입력한 경우 **/WEB-INF/applicationContext.xml 을 찾을 수 없다는 오류메세지**를 볼 수 있을 것이다.
 
 ### 예시1
~~~
 	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath*:egovframework/spring/context-*.xml</param-value>
	</context-param>
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
~~~	
### 예시2

 	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>
			/WEB-INF/context/context-datasoruce.xml
			/WEB-INF/context/context-aspects.xml
		</param-value>
	</context-param>
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
	
# DispatcherServlet

 > 기본적으로 **DispatcherServlet** 은 모든 Spring MVC 애플리케이션 의 진입 점이다 .   
 > 이것의 **목적**은 **HTTP 요청 을 가로 챈 다음 HTTP 요청을 처리하는 방법을 알 수있는 올바른 구성 요소에 요청을 전달하는 것**이다.  
 > 레거시 Spring 프로젝트 를 다루는 경우 XML 구성 을 찾는 것이 일반적 이며   
 > **Spring 3.1 까지는 DispatcherServlet 을 구성하는 유일한 방법  은 WEB-INF / web.xml 파일 을 사용하는 것이었다. ** 

    <servlet>
	<servlet-name>action</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/config/egovframework/springmvc/dispatcher-servlet.xml</param-value>
	</init-param>
	<load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
	<servlet-name>action</servlet-name>
	<url-pattern>*.do</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
	<servlet-name>action</servlet-name>
	<url-pattern>*.json</url-pattern>
    </servlet-mapping>
	
> **ContextLoaderListener** 에 해당하는 부분이 **root context** 가 되고  
> **DispatcherServlet** 에 해당하는 부분이 **child context** 가 된다.
