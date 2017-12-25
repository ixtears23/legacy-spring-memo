
Resolver
---

- ViewResolver 
  - RequestToViewNameTranslator
- MultipartResolver 
- LocaleResolver  
- ThemeResolver
- HandlerExceptionResolver


# ViewResolver 
* **기본값**은 `InternalResourceViewResolver`

> view 또는 view name이 사용자에 의해 정의되지 않으면  
> RequestToViewNameTranslator가 현재요청을 view name으로 변환합니다.  

## RequestToViewNameTranslator
* 해당 **bean이름**은 `viewNameTranslator`  
* **기본값**은 `DefaultRequestToViewNameTranslator`  


# MultipartResolver
> 멀티 파트 요청을 해결하기위한 디스패처의 전략은 `MultipartResolver` 구현에 의해 결정됩니다.  
> `Apache Commons FileUpload` 및 `Servlet 3`에 대한 구현이 포함되어 있습니다.  
* **일반적인 선택**은 `CommonsMultipartResolver` 이다.
* **빈의 이름**은 `multipartResolver`이다. 
* **기본값**은 `none`입니다.  


# LocaleResolver
> 로케일 해결 전략은 LocaleResolver에 의해 결정됩니다.  
> out-of-the-box 구현은 HTTP accept header, 쿠키 또는 세션을 통해 작동합니다.  
> out-of-the-box가 무슨말인 잘 모르겠지만.. [Versioning using Accept HTTP Header(Accept HTTP Header를 사용한 버전관리)](https://github.com/Microsoft/aspnet-api-versioning/issues/42)
* **빈의 이름**은 `localeResolver`입니다.  
* **기본값**은 `AcceptHeaderLocaleResolver`입니다.  

# ThemeResolver
> 테마 해결 전략은 ThemeResolver에 의해 결정됩니다.  
> 고정 테마 및 쿠키 및 세션 저장을위한 구현이 포함됩니다.  
* **빈의 이름**은 `themeResolver`이다.  
* **기본값**은 `FixedThemeResolver`입니다.  



# HandlerExceptionResolver
> Dispatcher의 예외 해결 전략은 HandlerExceptionResolver를 통해 지정할 수 있습니다.  
> 예를 들어 특정 예외를 오류 페이지에 매핑 할 수 있습니다.  
* **기본값**
1. ExceptionHandlerExceptionResolver  
2. ResponseStatusExceptionResolver  
3. DefaultHandlerExceptionResolver  
* **bean name**은 어떤것으로도 가능.
