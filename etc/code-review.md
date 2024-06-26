**[목차]**


이 글은 kokao tech에서 나온 “효과적인 코드리뷰를 위한 리뷰어의 자세” 글과 woowacon에서 나온 “우리 팀의 코드리뷰 문화, 이렇게 조금씩 발전했어요” 글을 참고하여 작성한 글입니다.

`리뷰어`: 다른 사람이 작성한 코드를 리뷰하는 사람

`리뷰이`: 본인이 작성한 코드를 다른 사람들에게 리뷰받는 사람

## 코드 리뷰란, 왜 해야 하는 걸까?

`코드 리뷰`란 한 개발자가 코드를 작성하면 **다른 개발자가 정해진 방법으로 피드백을 주고받는 과정**을 말합니다. 

이 과정을 통해 본인이 발견하지 못한 부분을 다른 사람이 발견하여 코드의 부작용과 오류를 조기에 대응할 수 있으며, 개발 내 정해진 컨벤션 규칙을 유지하고 기술 부채를 줄일 수 있습니다. 또한, 여러명의 개발자가 참여함으로써 문제 해결을 위한 기술 구현 방법론을 공유하기도 합니다.

즉, 코드리뷰를 하는 이유는 빠르네 팀내 코딩 스타일을  **정착**시키고, 코드의 **일관성**을 유지해야 하기 때문입니다.

효과적인 코드 리뷰를 지속하기 위해서는 리뷰어의 자세가 굉장히 중요한데, 리뷰의 5가지 규칙을 토태로 리뷰어가 어떤 자세로 임하면 좋을지 정리했습니다.

## 리뷰어의 5가지 규칙

### **1. 왜 개선이 필요한지 이유를 충분한 설명해 주세요.**

리뷰어가 코드 개선의 필요성을 느끼고 리뷰를 남긴다면 충분한 이유가 뒷받침되어야 합니다. 그래서 피드백을 작성할 때 리뷰이가 개선의 필요성을 느낄 수 있도록 구체적인 이유를 작성하면 좋습니다.

[안 좋은 리뷰]

```markdown
“data 변수 말고 다른 변수명으로 하세요."
“data 변수 말고 grade로 하세요.”
```

[좋은 리뷰]

```markdown
“data라는 이름은 현재의 자료구조가 무엇인지 그 의도를 알기가 어렵네요.
학점 정보를 담고 있는 자료구조 같은데 이와 관련된 변수명을 짓는다면
현재 정의한 자료구조가 무엇인지 그 의도를 쉽게 파악할 수 있을 것 같아요.”
```

위와 같이 개선이 필요한 이유를 구체적으로 설명하면서리뷰이가 스스로 생각하고 학습할 수 있도록 합니다.

### **2. 답을 알려주기보다는 스스로 고민하고 개선 방법을 선택할 수 있게 해주세요.**

답을 알려주기 보다는 키워드(filter)를 알려줌으로써 어떤 식으로 검색해야 하는지 방법을 제시합니다. 

이를 통해 리뷰이 입장에서는 동작 방식을 찾아보고 스스로 학습할 기회가 생기면서 비슷한 코드를 리팩터링할 수 있습니다.

[안 좋은 리뷰]

```markdown
“arr.filter(item => item % 2 === 0);으로 사용하세요."
```

[좋은 리뷰]

```markdown
“자바스크립트에는 배열에는 다양한 내장 메서드들이 존재합니다.
그중 filter 메서드를 활용해 보세요.
이 메서드를 활용하면 코드량을 줄일 수 있습니다.”
```

### **3. 코드를 클린 하게 유지하고, 일관되게 구현하도록 안내해 주세요.**

코드의 품질을 높이기 위해 개발자들은 항상 깨끗하게 코드를 유지하려고 노력을 많이 합니다. 클린 코드를 작성하는 방법은 다양하지만, **일관성 있게, 프로젝트에서 정한 컨벤션 규칙을 지키면서 코드를 작성하는게 좋습니다.** 

만약 프로젝트내 컨벤션 규칙이 없다면 본인이 정한 예상할 수 있는 수준의 컨벤션 규칙도 좋습니다.

리뷰이가 작성한 코드에서 일관되지 않은 부분은 알려주고 어떤 방식으로 수정하면 좋을지 방법을 제한하는 피드백입니다. 

[안 좋은 리뷰]

```markdown
"함수 표현식을 사용하셨군요. reduce의 사용도 잘 활용했네요."
```

[좋은 리뷰]

```markdown
"함수를 선언하는 두 가지 방식(함수 표현식, 함수 선언식)을 사용했는데
특별한 이유가 아니라면 함수를 선언하는 방식을 스스로 정하고 그 컨벤션 규칙을
따르도록 해보세요. 일관되게 동작하는 코드는 훨씬 보기 좋고 쉽게 수정할 수 있습니다.
그리고 reduce를 통해서 새로운 자료구조를 만든 건 잘했습니다.
하지만 같은 반복처리를 하는 과정에서 calculateEarningRate 에서
for문을 사용한 건 아쉽네요. reduce와 비슷한 방식의 다른 고차 함수를 찾아서
써보면 더 일관된 코드를 유지할 수 있을 거 같습니다."
```

### **4. 리뷰 과정이 숙제검사가 아닌 학습과정으로 느낄 수 있게 리뷰해 주세요.**

리뷰이가 코드 리뷰를 학습 일부로 받아들이기 위해 피드백을 자주 주고받고, 성장하고 있다는 생각을 심어주는게 좋습니다.

[안 좋은 리뷰]

```markdown

“클래스 상속은 필요 없습니다.”
```

[좋은 리뷰]

```markdown
"Component 클래스를 상속 받는 건 좋네요.
그러나 자식 클래스에서 부모 클래스를 호출만 하기 때문에 모든 클래스에서
상속받는 건 오히려 중복 코드 같아 보이기도 하는데 이렇게 작성해 주신 이유가 있을까요?"
```

### **5. 리뷰를 위한 리뷰를 하지 마세요. 피드백 할 게 없으면 칭찬해 주세요.**

리뷰할 부분이 없으면 칭찬 피드백을 해주는 것도 한 가지 방법입니다.

[칭찬 피드백에 대한 예시]

```markdown
- 코드량이 적당해서 읽기 편하네요.
- 많은 고민이 코드에서 엿보이네요.
- 성능에 아주 유리한 코드라고 생각되네요.
- 전에 코드보다 훨씬 좋아진 거 같네요.
- 예외 처리가 꽤 꼼꼼해서 좋네요.
- 함수, 변수명이 직관적이어서 좋네요.
```

## **추가 팁**

“작은 커밋 단위만을 보지 말고, 전체 코드의 맥락을 살피면서 리뷰를 해주세요.”

하나의 PR 안에는 작업 단위로 쪼갠 커밋들이 존재합니다. 따라서 정확한 리뷰를 위해서는 전체적인 코드의 맥락과 흐름을 파악하는 것이 좋습니다.

## 마치며..

코드 리뷰는 커뮤니케이션 비용이 많이 드는 일입니다. 큰 비용에도 불구하고 다양한 장점들이 존재하기 때문에 코드 리뷰는 꼭 하면 좋다고 생각합니다.

## 참고자료

- [kakao - 효과적인 코드리뷰를 위한 리뷰어의 자세](https://tech.kakao.com/2022/03/17/2022-newkrew-onboarding-codereview/)
- [woowabros - 우리 팀의 코드리뷰 문화, 이렇게 조금씩 발전했어요 (우아콘 2022)](https://www.youtube.com/watch?v=PBFUwGPp8DY)
