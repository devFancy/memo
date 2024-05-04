## @ConfigurationProperties, @ConstructorBinding 어노테이션

### @ConfigurationProperties

`@ConfigurationProperties` 어노테이션은 주로 application.properties 또는 application.yml 파일과 같은 외부 설정 파일에 선언된 속성들을 Java 객체에 매핑하기 위해 사용된다.

이 어노테이션은 **특정 prefix를 가지는 속성들을 한 개의 클래스에 모아 관리**할 수 있도록 도와준다.

> `prefix`란 @ConfigurationProperties 어노테이션에서 사용되는 용어로, Spring 설정 파일 내에서 특정 설정 그룹의 공통 경로를 지정하는 데 사용된다.
>
>  prefix는 설정 값들을 계층적으로 구조화하여 각 설정이 어떤 범주에 속하는지를 명시적으로 나타내는 역할을 한다.
>  예를 들어, `@ConfigurationProperties("oauth.google")` 어노테이션에서 `"oauth.google"` 부분이 prefix 이다.

예를 들어, `@ConfigurationProperties("oauth.google")`은 oauth.google으로 시작하는 모든 속성들을 해당 클래스의 필드와 매핑하도록 지시합니다. 
이렇게 함으로써 설정 값들을 객체 지향적인 방식으로 쉽게 관리하고 접근할 수 있게 됩니다.

### @ConstructorBinding

`@ConstructorBinding` 어노테이션은 `@ConfigurationProperties`와 함께 사용될 때, **생성자를 통한 의존성 주입을 활성화** 한다.

기본적으로 `@ConfigurationProperties`는 세터 메소드(setter)를 통해 프로퍼티 값을 주입받지만, `@ConstructorBinding`을 사용하면 **불변 객체를 만들 수 있으며, 모든 필드 값이 생성자를 통해 주입됨을 보장** 한다.

이는 `final` 키워드를 사용하여 객체의 불변성을 유지하는 데에도 도움이 되며, 필드 값이 한 번 설정된 후 변경되지 않도록 합니다. 생성자를 통한 바인딩은 코드의 안정성과 명확성을 높이는 데에 기여한다.

## 간단한 실습

> GoogleProperties.class

Google OAuth 서비스를 위한 여러 설정 값들을 담고 있는 클래스이다. 
- 각 필드에는 `@Value` 어노테이션을 통해 application.yml (또는 application.properties) 파일의 구체적인 키값이 명시되어 있으며, 이 값들은 생성자를 통해 주입된다.

```java
package com.hibitbackendrefactor.global.config.properties;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.context.properties.ConstructorBinding;

import java.util.List;

@ConfigurationProperties("oauth.google")
@ConstructorBinding
public class GoogleProperties {
    private final String clientId;
    private final String clientSecret;
    private final String oAuthEndPoint;
    private final String responseType;
    private final List<String> scopes;
    private final String tokenUri;
    private final String accessType;

    public GoogleProperties(@Value("${oauth.google.client-id}") final String clientId,
                            @Value("${oauth.google.client-secret}") final String clientSecret,
                            @Value("${oauth.google.oauth-end-point}") final String oAuthEndPoint,
                            @Value("${oauth.google.response-type}") final String responseType,
                            @Value("${oauth.google.scopes}") final List<String> scopes,
                            @Value("${oauth.google.token-uri}") final String tokenUri,
                            @Value("${oauth.google.access-type}") final String accessType) {
        this.clientId = clientId;
        this.clientSecret = clientSecret;
        this.oAuthEndPoint = oAuthEndPoint;
        this.responseType = responseType;
        this.scopes = scopes;
        this.tokenUri = tokenUri;
        this.accessType = accessType;
    }

    public String getClientId() {
        return clientId;
    }

    public String getClientSecret() {
        return clientSecret;
    }

    public String getOAuthEndPoint() {
        return oAuthEndPoint;
    }

    public String getResponseType() {
        return responseType;
    }

    public List<String> getScopes() {
        return scopes;
    }

    public String getTokenUri() {
        return tokenUri;
    }

    public String getAccessType() {
        return accessType;
    }
}
```

하지만 단순히 `@ConfigurationProperties`, `@ConstructorBinding` 어노테이션을 사용하면 아래와 같이 에러 메시지가 나오게 된다.

![](/img/ConfigurationProperties-error.png)

해당 내용은 `@EnableConfigurationProperties`를 통해 등록되지 않았거나 `@ConfigurationPropertiesScan`을 통해 검색되지 않는다는 내용이다.

Spring Boot 2.2 이후부터는 `@ConfigurationProperties`가 붙은 클래스를 스프링 컨텍스트에 등록하기 위해서는 추가적인 설정이 필요하게 되었다. 이런 경우에는 아래와 같은 세 가지 방법 중에 하나를 사용하면 된다.
- 1. `@EnableConfigurationProperties`: 이 어노테이션을 사용하여 구성 클래스에서 특정 `@ConfigurationProperties` 클래스(또는 클래스들)를 명시적으로 활성화할 수 있다.
예를 들어, `@EnableConfigurationProperties(GoogleProperties.class)`와 같이 사용할 수 있다.

- 2. 스프링 컴포넌트로 등록: `@ConfigurationProperties`가 붙은 클래스에 `@Component`와 같은 스테레오타입 어노테이션을 추가하여 스프링 빈으로 등록할 수 있다.

- 3. `@ConfigurationPropertiesScan`: Spring Boot 2.2에서 새롭게 도입된 이 어노테이션을 사용하면 `@ConfigurationProperties`가 붙은 클래스를 스캔 대상으로 지정할 수 있다. 
이 어노테이션을 구성 클래스에 추가하면 지정된 패키지 내의 모든 `@ConfigurationProperties` 클래스가 자동으로 스캔되어 빈으로 등록된다.

### 해결 - EnableConfigurationProperties

필자는 첫 번째 방법을 사용했다. 그래서 PropertiesConfig 라는 클래스를 생성하여 아래와 같이 구성했다.

```java
package com.hibitbackendrefactor.global.config;

import com.hibitbackendrefactor.global.config.properties.GoogleProperties;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableConfigurationProperties(GoogleProperties.class)
public class PropertiesConfig {
}
```

그러면, `ConfigurationProperties` 어노테이션에서 에러 메시지가 뜨지 않고, 정상적으로 처리된다.
