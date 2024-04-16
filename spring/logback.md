# Logback

## 로깅을 하는 이유

로깅이란 시스템이 동작할 때 **시스템의 상태 및 동작 정보를 시간 경과에 따라 기록하는 것**을 의미한다.
로깅을 통해 개발자는
- 개발 과정 혹은 개발 후에 발생할 수 있는 예상치 못한 애플리케이션의 문제를 진단할 수 있다.
- 다양한 정보를 수집할 수 있다.
- 사용자 로그의 경우 분석 데이터로도 활용할 수 있다.

하지만, 로깅을 하는 단계에서 적절한 수준의 로그 기록 기준을 잡지 못하면, **방대한 양의 로그 파일이 생성되는 문제**를 겪거나, **의미 있는 로그를 쌓지 못하는 경우가 발생할 수 있다.**  -> 이러한 문제를 해결하기 위해 효율적으로 로깅을 하는 방법을 이해하는 것이 중요하다.


## LogBack이란

`Slf4j`의 구현체로 Spring Boot 환경이라면 별도의 의존성 추가 없이 기본적으로 포함되어 있다.
- `Logback`은 `Log4j`에 비해 향상된 필터링 정책, 기능, 로그 레벨 변경 등에 대해 서버를 재시작할 필요 없이 자동 리로딩을 지원한다는 장점을 가진다.

## 로그 레벨

로그의 레벨은 총 5가지 이며, 아래와 같다.
- `Error` : 예상치 못한 심각한 문제가 발생한 경우
- `Warn` : 로직 상 유효성 확인, 예상 가능한 문제로 인한 예외 처리
- `Info` : 운영에 참고할 만한 사항
- `Debug` : 개발 단계에서 사용하며 SQL 로깅을 할 수 있다.
- `Trace` : 모든 레벨에 대한 로깅이 추적 (개발 단계에서 사용)

위의 5가지에 대한 심각도 수준 순서는 아래와 같다.
Error > Warn > Info > Debug > Trace
- 만약 로그 레벨을 `Info`로 설정 시, `Info` 레벨 이상의 로그 레벨인 `Warn`, `Error`` 만 출력된다. 

## LogBack 설정 방법

SpringBoot 환경이라면 별도의 설정없이 사용이 가능하다.
로그 관련 설정 방법은 `application.yml` 과 `logback-spring.xml` 에서 설정하는 방법이 있다.

`application.yml`은 기본 설정 난이도가 비교적 쉽지만, 세부적인 설정이 불편하기 때문에, `logback-spring.xml` 으로 관리하는 편이 더 좋다고 한다. 따라서 `logback-spring.xml` 으로 로그를 기록해보자.

`resources` 패키지에 `logback-spring.xml`을 생성한다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<configuration>
		<!-- base.xml default.xml 에 존재하는 Log 메시지의 Color 설정 -->
    <conversionRule conversionWord="clr" converterClass="org.springframework.boot.logging.logback.ColorConverter"/>
		
	<!-- 콘솔에 출력되는 로그 패턴 -->
    <property name="CONSOLE_LOG_PATTERN"
              value="%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %clr(%5level) %cyan(%logger) - %msg%n"/>
		<!-- Log파일에 기록되는 로그 패턴 -->
    <property name="FILE_LOG_PATTERN" value="%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %5level %logger - %msg%n"/>
		
	<!-- 콘솔로그 Appender -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>${CONSOLE_LOG_PATTERN}</pattern>
        </encoder>
    </appender>
		
	<!-- 파일로그 Appender -->
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <encoder>
            <pattern>${FILE_LOG_PATTERN}</pattern>
        </encoder>
		<!-- RollingPocliy: 로그가 길어지면 가독성이 떨어지므로 로그를 나눠서 기록하기위한 규칙 -->
		<!-- 로그파일을 크기, 시간 기반으로 관리하기 위한 SizeAndTimeBasedRollingPolicy -->
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
			<!-- 로그파일명 패턴 -->
			<!-- 날짜별로 기록되며 maxFileSize를 넘기면 인덱스(i)를 증가시켜 새로운 이름의 로그파일에 기록을 이어간다 -->
            <fileNamePattern>./log/%d{yyyy-MM-dd}.%i.log</fileNamePattern>
			<!-- 로그파일 최대사이즈 -->
            <maxFileSize>100MB</maxFileSize>
			<!-- 생성한 로그파일 관리 일수 -->
            <maxHistory>30</maxHistory>
        </rollingPolicy>
    </appender>

	<!-- local Profile에서의 로그 설정 -->
    <springProfile name="local">
		<!-- 해당 패키지의 로그는 DEBUG 레벨 부터 출력 -->
        <logger name="com.chiwawa.lionheart" level="DEBUG" />
		<!-- 전체적인 로그는 INFO 레벨 부터 출력 -->
        <root level="INFO">
			<!-- CONSOLE 로그 Appender를 로그 Appender로 등록 -->
            <appender-ref ref="CONSOLE" />
        </root>
    </springProfile>
	<!-- dev Profile에서의 로그 설정 -->
    <springProfile name="dev">
        <root level="INFO">
            <appender-ref ref="CONSOLE" />
            <appender-ref ref="FILE" />
        </root>
    </springProfile>
	<!-- prod Profile에서의 로그 설정 -->
    <springProfile name="prod">
        <root level="INFO">
            <appender-ref ref="CONSOLE" />
            <appender-ref ref="FILE" />
        </root>
    </springProfile>

</configuration>
```

세부적인 내용은 필요에 따라 아래 참고 자료를 통해 확인하자.



## 참고 자료

- [Logback 으로 쉽고 편리하게 로그 관리를 해볼까요? ⚙️](https://tecoble.techcourse.co.kr/post/2021-08-07-logback-tutorial/)
- [LogBack을 통한 효율적인 로그 관리](https://velog.io/@pgmjun/LogBack%EC%9D%84-%ED%86%B5%ED%95%9C-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-%EB%A1%9C%EA%B7%B8-%EA%B4%80%EB%A6%AC)
