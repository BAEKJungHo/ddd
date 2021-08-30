# CQRS(Command and Query Responsibility Segregation)

SI 에서 일할때, `순환참조` 문제를 겪은 적이 있다. A service 에서 B service 를 의존하고, B 에서는 A 를 의존하여 발생했던 문제인데,
A 에서는 B 에 있는 조회를 사용하고, B 에서 등록할때 A 도 같이 등록하는 경우 였던거같다.

이러한 순환참조는 보통 `설계가 잘 못되었을때 발생`하는데, 가장 좋은 방법은 설계를 다시 하는 것이다. 그리고 설계할때 CQRS 를 적용하면 순환참조 발생 가능성이 낮아진다.

즉, 명령과 쿼리를 분리하는 것이다. A service 에서는 B service 의 명령 작업이 필요없는데 굳이 A service 에서 B 의 명령 함수들 까지 노출시킬 필요가 없기 때문이다.

또한 명령과 쿼리를 분리한 서비스에서 트랜잭션 기본 설정을 다음과 같이 할 수 있다.

- 명령은 `@Transcational`
- 쿼리는 `@Transactional(readOnly = true)` 

> [복잡한 쿼리는 리드모델로](https://github.com/BAEKJungHo/driven/blob/main/ddd/%EB%8F%84%EB%A9%94%EC%9D%B8%20%EC%A3%BC%EB%8F%84%20%EC%84%A4%EA%B3%84%20%EC%B2%A0%EC%A0%80%20%EC%9E%85%EB%AC%B8/13.%20%EB%AA%85%EC%84%B8(Specification).md#%EB%B3%B5%EC%9E%A1%ED%95%9C-%EC%BF%BC%EB%A6%AC%EB%8A%94-%EB%A6%AC%EB%93%9C%EB%AA%A8%EB%8D%B8%EB%A1%9C)
