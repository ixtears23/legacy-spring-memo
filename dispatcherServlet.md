> 웹 애플리케이션은 **여러 개의 DispatcherServlet을 정의 할 수 있습니다.**  
> **각 서블릿**은 **자체 네임 스페이스에서 작동**하며 매핑, 처리기 등으로 자체 응용 프로그램 컨텍스트를로드합니다.  
> `ContextLoaderListener`에 의해로드 된 **루트 응용 프로그램 컨텍스트 (있는 경우) 만 공유**됩니다.


> Spring 3.1부터, DispatcherServlet은 자체적으로 내부적으로 생성하는 것이 아니라  
> 웹 애플리케이션 컨텍스트와 함께 삽입 될 수 있습니다.  
> 이는 서블릿 인스턴스의 프로그래밍 방식 등록을 지원하는 Servlet 3.0 이상의 환경에서 유용합니다.  
> 자세한 내용은 DispatcherServlet (WebApplicationContext) javadoc을 참조하십시오.  
> 이하 DispatcherServlet (WebApplicationContext) javadoc

##### 생성자 `public DispatcherServlet(WebApplicationContext webApplicationContext)`  

> 이 생성자를 사용하면 다음 속성 / init-params가 무시된다는 것을 나타냅니다.  
* FrameworkServlet.setContextClass(Class) / 'contextClass'
* FrameworkServlet.setContextConfigLocation(String) / 'contextConfigLocation'
* FrameworkServlet.setContextAttribute(String) / 'contextAttribute'
* FrameworkServlet.setNamespace(String) / 'namespace'

> 주어진 웹 응용 프로그램 컨텍스트는 아직 갱신되지 않았거나 갱신되지 않을 수 있습니다.  
> 아직 새로 고치지 않은 경우 (권장 방법) 다음이 발생합니다.  
* 지정된 컨텍스트에 부모가없는 경우, 루트 어플리케이션 컨텍스트가 부모로서 설정됩니다.  
* 지정된 컨텍스트에 ID가 할당되어 있지 않은 경우, 그 ID에 할당 할 수 있습니다.  
* ServletContext 및 ServletConfig 객체가 응용 프로그램 컨텍스트에 위임됩니다.  
* [FrameworkServlet.postProcessWebApplicationContext (org.springframework.web.context.ConfigurableWebApplicationContext)](https://docs.spring.io/spring/docs/5.0.3.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/servlet/FrameworkServlet.html#postProcessWebApplicationContext-org.springframework.web.context.ConfigurableWebApplicationContext-)가 호출됩니다.  
* "contextInitializerClasses"init-param 또는 [FrameworkServlet.setContextInitializers (org.springframework.context.ApplicationContextInitializer <?> ...)](https://docs.spring.io/spring/docs/5.0.3.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/servlet/FrameworkServlet.html#setContextInitializers-org.springframework.context.ApplicationContextInitializer...-) 속성을 통해 지정된 모든 ApplicationContextInitializers가 적용됩니다.  
* 컨텍스트가 [ConfigurableApplicationContext](https://docs.spring.io/spring/docs/5.0.3.BUILD-SNAPSHOT/javadoc-api/org/springframework/context/ConfigurableApplicationContext.html)를 구현하는 경우 [refresh()](https://docs.spring.io/spring/docs/5.0.3.BUILD-SNAPSHOT/javadoc-api/org/springframework/context/ConfigurableApplicationContext.html#refresh--)가 호출됩니다.
* If the context has already been refreshed, none of the above will occur, under the assumption that the user has performed these actions (or not) per their specific needs.

> 사용 예제는 [WebApplicationInitializer](https://docs.spring.io/spring/docs/5.0.3.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/WebApplicationInitializer.html)를 참조하십시오.

