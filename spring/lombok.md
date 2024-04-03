## Lombok 관련 어노테이션 정리

### @Accessors

- @Setter를 이용해서 객체를 생성할 때에는 여러 줄로 setMethod를 생성해야 하는 단점이 존재한다.
-> 이러한 단점을 보완하기 위해 @Accessors(chain = true)를 사용한다.

- 장점을 정리하면, 일일이 setMethod를 여러 줄로 생성할 필요 없이 위와같이 Chain 형태로 이어서 원하는 setMethod를 생성할 수 있다.

- @Accessors(chain = true) 에 대한 예시
  - Person person  = new Person().name("fancy").age(30);

[참고자료] - https://djlee118.tistory.com/474

---

### @JsonInclude

- json 형식으로 데이터를 주고받을 때, Jackson의 ObjectMapper를 자주 이용한다.
기본값으로 Serialize 하게 되면, null, "" 같은 필요 없는 값 또한 모두 변환시켜준다.
이를 아래의 메서드를 통하여 Serialize 할 때 원하는 값만을 포함시킬 수 있다.

예시.  @JsonInclude(value = JsonInclude.Include.NON_NULL)

#### Include 옵션 -> 데이터를 json으로 변환한다.

- ALWAYS(기본값) : 모든 값을 출력한다.
  - 예시. @JsonInclude(value = JsonInclude.Include.ALWAYS)

- NOT_NULL : null 값을 제외한 값을 출력한다.
  - 예시. @JsonInclude(value = JsonInclude.Include.NON_NULL)

- NON_ABSENT : null / AtomicReference를 제외한 값들만 출력한다. 

- NON_EMPTY : NULL / ABSENT / Collection / Map / Array / String이 NULL이거나 0인 데이터를 제외한 값을 출력한다.


### @JsonProperty

- 서버에서는 카멜 케이스(phoneNumber), 클라이언트에서는 스네이크 케이스(phone_number) 방식을 사용한다. 여기서 서버와 클라이언트가 데이터를 통신할 때 JSON 형식을 주로 사용하는데, key 이름과 변수명이 다른 문제가 발생할 수 있다. 즉, 표현 방식이 달라지는 경우가 존재한다. 이러한 문제를 해결할 때, JsonProperty, JsonNaming 어노테이션을 사용한다.

- 객체의 JSON 형식으로 변환할 때, Key의 이름을 설정할 수 있다.

> 예시

```java
@Data
public class User {
    @JsonProperty("user_id")
    private String userId;

    @JsonProperty("user_pw")
    private String userPw;

    @JsonProperty("phone_num")
    private String phoneNum;
}
```
- @JsonProperty 어노테이션을 통해 JSON 변환 시 받을 key 값을 설정한다.
해당 어노테이션을 적용한 후 API 테스트를 진행해보면, 클라이언트의 데이터가 정상적으로 넘어온 것을 확인할 수 있다.

[참고자료] - https://yeonyeon.tistory.com/65

### @JsonNaming

- 위의 JsonProperty 에서는 한 개의 필드에 적용하는데, 만약 여러 개의 필드를 적용하는 경우에는 JsonNaming 어노테이션을 사용하면 된다.

> 예시

```java
@JsonNaming(value = PropertyNamingStrategy.SnakeCaseStrategy.class)
public class User {
    private String userId;
    private String userPw;
    private String phoneNum;
}
```
