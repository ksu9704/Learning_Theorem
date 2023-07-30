## REST API



### API를 왜 사용하고 어떻게 사용할까?

모놀리식 애플리케이션이 완전히 사라졌다거나 앞으로도 만들어지지 않는다는 말은 아니다. 특희 다음과 같은 환경에서는 다양한 상황에서 단일 패키지로 수많은 기능을 제공하는 모놀리식 애플리케이션이 여전히 유효하다.

- 도메인과 도메인의 경계가 모호할 때
- 제공된 기능이 긴밀하게 결합됐으며, 모듈 간 상호작용에서 유연함보다 성능이 절대적으로 더 중요할 때
- 관련된 모든 기능의 애플리케이셔 확장 요구사항이 알려져 있고 일관적일 때
- 기능이 변동성이 없을때, 즉 변화가 느리거나 변화 범위가 제한적일 때와 둘 다일 때

그 외에는 MAS(마이크로서비스)를 사용한다.

물론 이 요약은 지나치게 단순화됐지만 타당하다. 마이크로서비스에서는 기능을 작고 응집역 있는 **청크**로 분할해 디커플링한다. 따라서 더 빠른 배포롸 용이한 유지보수가 가능한 우연하고 튼튼한 시스템을 구축하게 된다.

어떤 마이크로서비스 분산 시스템에서든 통신이 핵심이다. 어떤 서비스도 섬처럼 고립되어 동작하지 않는다. 애플리케이션/마이크로서비스를 연결하는 수많은 동작 방식이 있지만, 일상생활에서 자주 사용하는 인터넷으로 이야기를 시작해보겠다.

이터넷은 통신을 위한 수단으로 만들었다. 인터넷의 전신인 **AROANET**의 설계자들은 '중대한 장애'가 발생하더라도 시스템 간 통신이 유지되게 하려고 했다. **AROANET과 HTTP** 기반의 접근방식은 유사하다. 오늘날 사용하는 시스템은 유선을 통해 다양한 리소스를 생성, 조회, 업데이트, 삭제하는 등의 기능을 수행한다.

</br>

### REST가 무엇이며, 왜 중요한가?

앞서 말했다 싶이, API는 개발자 작성한 사양/인터페이스이다. 

- API를 통해 라이브러리
- 다른 어플리케이션
- 서비스 같은 코드

들을 사용 할 수있다. 그런데 **REST API**에서 REST의 의미는 무었일까?

REST는 Representational State Transfer의 약어이다. 다소 모호한 표현이지만 다음과 같이 설명한다. 

> 애플리케이션 A가 애플리케이션 B와 통신할 때, A는 B에서 통신 시점의'현재 상태'를 가져온다. A는 B가 통신 호출간 '상태'를 유지하라고 가정하지 않는다. A는 B에 요청할 때마다 관련 '상태'의 표현을 제공한다. 이런 동작 방식은 생존가능성과 회복탄력성을 향상시킨다. 이렇게 처리하는 이유는 통신 문제가 발생하거나 B가 충돌해 재시작돼도, A와 상호작용한 연재상태를 잃어버리지 않기 때문이다. A가 다시 요청해 두 애플리케이션이 중단된 곳에서 통신을 이어간다.



</br>

### API, HTTP 메서드 스타일

**IETF RFC**문서에 수많은 표준 HTTP 메서드가 정의됐다. 그중 API를 만들 때 일반적으로 사용되는 것은 일부이며, 가끔 사용되는 메서드가 몇 개 더 있다. REST API는 주로 다음의 HTTP 메서드를 기반으로 한다.

- POST
- GET
- PUT
- PATCH
- DELETE

이는 생성(POST), 읽기(GET), 업데이트(PUT 및 PATCH), 삭제 (DELETE) 와 같이 리소스에 수행하는 일반적인 작업이다. 때로는 다음의 두 메서드도 사용한다.

- OPTIONS
- HEAD

두 메서드는 요청/응다 쌍에서 사용할 수 있는 통신 옵션을 조회하고(OPTIONS), 응단 메시지에 바디를 뺀 응답 헤더를 조회하는(HEAD)데 사용한다.

</br>

### GET
