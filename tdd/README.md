# Test Driven Development

- [https://tddmanifesto.com/](https://tddmanifesto.com/)
- [https://www.guru99.com/test-driven-development.html](https://www.guru99.com/test-driven-development.html)
- [https://www.browserstack.com/guide/what-is-test-driven-development](https://www.browserstack.com/guide/what-is-test-driven-development)

## What is TDD

TDD에 관한 가장 큰 오해는 TDD를 설계에 대해 고려하지 않고 코드를 작성하는 code-and-fix로 생각하는 것입니다. 

__TDD는 단순하게 설계와 무관하게 구현만 하는 것이 아니라 가장 단순한 설계에 이를 수 있도록 시스템이 제공해야 하는 기능을 Test Case의 형식으로 작성하고, 기능을 통과시키기 위한 가장 단순한 솔루션을 통해 Test Case를 통과시킨 후, 통과한 Test Case를 regression test의 용도로 삼아 최적의 설계를 얻기 위해 구체적인 코드를 보며 리팩토링을 하는 과정입니다. TDD란 Ron Jeffries가 말한 것처럼 작동하는 가장 단순한 솔루션을 만드는 가장 효과적인 방법이라고 할 수 있습니다.__

TDD는 모델을 만들어 주지 않습니다. 모델은 프로젝트에 참여한 사람들 간의 긴밀한 협력과 도메인에 대한 분석을 통해 만드는 것이지 TDD를 통해 만들어 지는 것이 아닙니다. 이것은 어떤 방법을 사용하더라도 마찬가지입니다. 즉, 공통의 모델을 만들기 위한 노력이 없다면 사전 설계 후에 구현에 들어간다고 해도 프로젝트 관련자들 간에 공유할 수 있는 모델을 만드는 것은 불가능합니다. 이것은 UML을 사용해서 다이어그램을 그린다고 해서 모델이 만들어지지 않는 것과 동일한 것이죠.

TDD는 단순하면서도 고품질의 소프트웨어를 구현하기 위한 방법이지 모델을 만들기 위한 방법이 아닙니다. DDD와 TDD는 이름만 유사할 뿐 서로 완전히 다른 레벨의 개념이며 비교할 필요가 없는 것이죠. TDD는 그것이 도메인에 관계된 것이건, 기술적인 인프라스트럭처에 관계된 것이건 어떤 대상을 구현하기 위한 방법일 뿐입니다.

단순히 TDD를 한다고 해서 무조건 좋은 모델이 만들어진다고 주장하는 사람은 없습니다. __다만 사전 설계에 비해 TDD를 통해 더 단순하고 품질이 높은 설계를(모델이 아니라) 얻는다는 것이죠.__ 따라서 "TDD가 모델을 만들어 준다는 건 동의할 수 없다"는 말씀은 허수아비 공격의 오류라고 할 수 있습니다.

__그러나 모델을 만들기 위한 전제조건이 갖추어 졌을 경우 모델을 코드로 구현하기 과정에 있어서 TDD를 적용하는 것은 효과적이라고 생각합니다. 그것은 아무런 구체적인 피드백 없이 머릿속으로 사전설계를 하는 것에 비해 구체적인 코드로부터의 피드백을 활용할 수 있는 TDD가 더 적절한 설계의 모델을 얻을 수 있기 때문이죠.__ 이것은 Model-Driven Design을 달성하는 좀 더 쉬운 방법이라고 생각합니다. 실제로 구현을 해봐야 모델과 구현 간에 일관성 여부를 확인할 수 있을 테니까요.

> http://aeternum.egloos.com/2422827

## 단위테스트가 아닌 TDD 로 코드 구현을 현업에서 많이 사용할까?

> 조영호님 답변

TDD를 하기 위해서는 좋은 설계에 대한 감각을 가져야 하는데 이러한 감각이 결여되어 있을 경우 TDD를 한다고 해서 (안 하는 것 보다는 나을지 몰라도) 여전히 좋은 설계를 만들 수는 없기 때문이기도 하고, TDD를 설계가 아닌 단위 테스트 작성의 용도로 생각하시는 경향으로 인해 좋은 설계보다는 테스트 커버리지를 높이기 위한 관점에서 접근하는 경우가 종종 있기 때문이기도 합니다. 레거시 코드가 TDD에 걸림돌이 되는 경우도 있고요.

## RED-GREEN-REFACTOR

> 보통 실무에서는 RED-GREEN-REFACTOR 를 한 단위로 묶어서 PR 한다.

## 책 추천

- __테스트 주도 설계__
  - http://kangcom.com/sub/view.asp?sku=200412020003
  - 예제는 간단하지만 TDD의 흐름에 관해 가장 적절한 설명을 담고 있습니다.
- __Test Driven:TDD and Acceptance TDD for Java Developers__
  - http://www.amazon.com/Test-Driven-Acceptance-Java-Developers/dp/1932394850
  - 이 책의 2장과 3장은 TDD와 리팩토링을 이해할 수 있는 깔끔한 예제를 제공하고 있습니다.
- __Growing Object-Oriented Software, Guided by Tests__
  - http://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627/ref=sr_1_1?ie=UTF8&s=books&qid=1286948027&sr=1-1
  - TDD를 통해 객체 지향적인 도메인 레이어를 구현하는 방법에 관해 배울 수 있습니다.
- __패턴을 활용한 리팩터링__
  - http://kangcom.com/sub/view.asp?sku=200607110007
  - 1장을 읽어 보시길 권합니다. 
