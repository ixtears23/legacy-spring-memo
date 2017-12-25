
# log4j2  

[[apache log4j2]](https://logging.apache.org/log4j/2.x/)


### 로깅 피크 처리량  
> 64 스레드의 테스트에서   
> Loggers all async(비동기) 는 Async Appender의 12배, Sync의 64배  
> Async Appender  
> Sync(동기)  


> Log4j 2는 기존 Properties 파일 형식의 환경 설정을 지원하지 않으며,  
> XML (log4j2.xml) 혹은 JSON (log4j2.json or log4j2.jsn) 파일 형식의 환경 설정만 가능하다.  

##### XML 파일 위치  
> XML 파일 (log4j2.xml)을 작성하고, `WEB-INF/classes` 하위에 포함될 수 있도록 위치시킨다.  
> Log4j 2가 초기화될 때 자동으로 위 설정 파일을 읽어들인다.  

##### XML 파일 정의  
> Log4j 2에서는 XML 파일의 최상위 요소가 `<Configuration>`으로 변경되었다.  
> `<Configuration>`요소 아래에 `Logger, Appender, Layout` 설정 등과 관련한 하위 요소를 정의한다.  


## 실제 테스트

> 아래코드는 기본이랄까?  
> 더 찾아봐야 함.
> log4j apache에 가보면 많이 있음...

`WEB-INF/classes/log4j2.xml`
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
  <Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
      <PatternLayout pattern="%d %-5p [%t] %C{2} (%F:%L) - %m%n"/>
    </Console>
  </Appenders>
  <Loggers>
    <Logger name="spring.learning.spring.dori.controller" level="info"/>
    <Root level="debug">
      <AppenderRef ref="STDOUT"/>
    </Root>
  </Loggers>
</Configuration>
~~~

## library에 추가한 jar파일
> log4j-1.2-api-2.10.0.jar  
> log4j-api-2.10.0.jar  
> log4j-core-2.10.0.jar  

