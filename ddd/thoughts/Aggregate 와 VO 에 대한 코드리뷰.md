# Aggregate 와 VO 에 대한 코드리뷰

> "고객의 최종 웨이팅이 아직 대기중이면 신규 웨이팅을 추가하지 못한다"
라는 비즈니스 로직에 대한 검증이 Waiting을 통해 이루어 지지 않을 경우
로직이 한곳에 잘 응집되지 못하고 파편화 되었다고 생각될 수 도 있을 것 같아용

이 부분 정확하게 짚어주신것 같아요. 저도 리팩토링 진행하면서 같은 생각이었습니다. 본래 `예약 상태`는 Waiting 에 종속적이라고 보여집니다. 하지만 WaitingTransaction 을 둔 이유가 `상태가 자주 변하며`, 자주 변하는 상태를 추적하기 위해 `History Table` 처럼 관리하기 위해 분리된게 아닐까 생각합니다. 

> 다만 웨이팅에서의 웨이팅 상태 기록의 경우에는 전역식별자(PK가 있긴하지만 용도가 전역적으로 식별할 용도는 아니라고 생각됨, Value가 바뀔 수 없을 뿐더러 Value가 바뀌었을 때 동일한 객체라고 생각하기도 힘듦 => 오히려 VO에 가까운 녀석이 아닐까? 라는 생각이 듭니다)

WaitingTranscation 을 VO 에 가까운 녀석이지 않을까라고 말씀해주셨는데, 이 부분은 전혀 아니라고 생각합니다. 

<s>__VO 는 반드시 불변이어야 합니다.__</s>

> VO 가 불변이어야 한다는 것은 맞지만, (물론 특정 상황에 따라서는 VO 도 변할 수 있다고 합니다.) 줄을 그은 이유는, 제가 WaitingTranscation 이 왜 VO 가 아닌지에 대한 설명으로는 부적절하다고 판단했습니다.

예를 들어, 고객이나 주문과 같은 도메인 개념들은 시간에 따라 상태가 변경됩니다. 

WaitingTransaction 도 상태가 계속 변하는 녀석입니다. `상태 변경 이력 관리` 차원에서 테이블이 분리된 것이지 `예약 상태`는 본래 Waiting 에 종속적인 것이므로, 예약이라는 도메인이 불변일 수 없는 것처럼, WaitingTransaction 또한 VO 가 될 수 없다고 생각합니다. 

객체 탐색을 시작하기 위한 `진입점(Entry Point)`은 항상 REFERENCE OBJECT 여야 합니다. <s>현재 Waiting Entity 의 transcations 를 보시면 될 것같습니다. </s>

따라서, WaitingTranscation 이 왜 생겼는지와 현재 엔티티의 설계적인 부분을 고려했을때

__WaitingTransaction 은 VO 가 아닌 REFERENCE OBJECT 입니다.__

---

> 추가적인 이해를 돕기 위해, Eric Evans 의 도메인 주도 설계. Aggregate 내용과 블로그를 참고하여 작성합니다. 

![waitingddd](https://user-images.githubusercontent.com/47518272/158015730-48d57d88-8286-4034-b9ed-cc14020620c1.png)

> 웨이팅 상태 기록의 경우에는 전역식별자(PK가 있긴하지만 용도가 전역적으로 식별할 용도는 아니라고 생각됨, 

- `전역 식별자`라는 명칭은 Aggregate 내의 Root(Entry Point) 에만 해당됩니다.
- Root 를 제외한 Aggregate 내의 REFERENCE OBJECT 들은 `지역 식별자`를 갖습니다.

> WaitingTransaction의 대한 Repository가 생성되는 것이 맞을까 라는 생각을 했었던 것 같아용

이 부분은 동규님이 생각하신게 맞다고 저도 생각합니다.

- 오직 ENTRY POINT 만이 REPOSITORY 로부터 직접 얻어질 수 있다.
- 다른 객체들은 ENTRY POINT 로 부터 객체 탐색을 통해 얻어질 수 있다.

> 오히려 VO에 가까운 녀석이 아닐까? 라는 생각이 듭니다

도메인 주도 설계 책에서는 다음과 같이 설명이 되어있습니다.

__VALUE OBJECT 는 불변적(immutable)으로 다뤄라. 아무런 `식별성`도 부여하지 말아라__

### VO 를 식별하기 위해 도움이 되는 질문

- __개체를 동일한 속성을 가진 다른 개체로 바꿀 수 있습니까?__
- __시간이 지나면서 무언가를 추적해야 합니까?__

이미 WaitingTransaction 은 History Table 로서 상태값과, Description, 그리고 식별자를 갖기 때문에 VO 로 보긴 힘들것 같습니다.
