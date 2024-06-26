# [일의 난이도 높이기](https://jojoldu.tistory.com/701) + 생각

위의 “일의 난이도 높이기”라는 향로님의 기술 블로그를 읽으면서 정리한 내용입니다. 끝에는 저의 현재 상황 속에서 어떻게 개선해볼지 간략히 정리했습니다.

## 글 정리

- 익숙한 일이 반복된다면, 그때가 그동안 내가 익히지 못했던 여러 개선 방법드를 시도할 때 여러 개선 방법들을 시도할 때
    - 기존의 레거시된 코드를 리팩터링하기
    - 기존에 기능 구현에 집중했다면 → TDD로 해당 기능을 구현해보기
    - 자바 예전 문법(Java 6-7)으로 했다면 → 람다, 스트림 같은 Java 8 문법부터 함수형 프로그래밍 관련 문법을 적용해보기
    - 단위 테스트 도입 이후에 통합 테스트 작성하면서 테스트 커버리지 비율 높이기
- 지금 하고 있는 일이 점점 익숙해지고 있다면, 일의 난이도를 높여보기
    - 어떻게 하면 기존에 하던 방법을 더 빠르게 구현할 수 있을까
    - 어떻게 하면 더 좋은 방법으로 구현할 수 있을까
- 익숙한 일을 익숙하지 않는 방법으로 해결해볼 수록 성장할 수 있다.
    - TDD, IDE의 단축키, 단위 테스트 전환, API Dos(Swagger) 등 그간 해보고 싶었지만 못했던 여러 방법들을 시도해볼때

## 현재 상황(24.04.16)

- **현재 회사 상황**에서의 일의 난이도 높이기
    - 레거시된 코드를 리팩터링하기 (람다와 스트림 문법 적용하기)
    - API 문서를 위해 Swagger/Spring Rest Docs 적용하기(현재 상황에서는 Rest Docs로 하기는 어려움)
    - 빌드 및 배포 파이프라인을 설계하여 자동화하는 것으로 개선하기 (수동 → 자동화)
    - 이러한 난이도 높이는 것은 기본적인 일을 끝내놓고 난 이후에 진행 할 것
        - 예외) 회사에서 이러한 작업을 업무 시간에 허용해주면 더더욱 열심히 해보자 !

## 참고자료

- [일의 난이도 높이기](https://jojoldu.tistory.com/701)
- [혼란함에 익숙해지기](https://jojoldu.tistory.com/770)