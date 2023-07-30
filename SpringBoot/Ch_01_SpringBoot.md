## 스프링 부트의 핵심 기능

스프링 부트의 세가지 핵심 기능이 있다.
이처럼 스프링 부트의 모든 기능은 이 세 가지 핵심 측면을 기반으로 한다.

- 의존성 관리 간소화
- 배포 간소화
- 자동 설정 



### 의존성 관리 간소화 - 스타터

스프링 부트의 특별한 점은 '의존성'을 수월하게 관리 한다는 것이다.
일반적으로 애플리케이션에서 제공하는 모든 기능에는 여러 기본 의존성이 필요하다.

**예를 들자면** RESTful Web API를 개발하는 경우 HTTP 엔드포인트를 만들어 요청을 수신하고, 요청을 처리할 메서드/함수에 해당 엔드포인트를 연결한 후에 적절한 응답을 만들어 반환한다. 대부분의 기본적인 의존성은 기능 구현을 위해 추가로 설정해야 하는 수많은 의존성을 이미 포함한다.

##### 가령 RESTful Web API는 아래와 같은 의존성을 포함한다.

- 특정 형식으로 응답하는 코트(JSON, XML, HTML)
- 요청된 포맷의 객체를 마샬링/얼마샹링하는 코드
- 요청을 처리하고 다시 응답을 반환하는 코드와 다양한 유선 프로토콜 등을 지원하는 코드

이처럼 RESTful Web API 같은 매우 간단한 예시에도 빌드 파일에 수많은 의존성이 필요하며, 심지어 여기서는 오직 외부 상호작용만을 고려하고 애플리케이션에 어떤 기능을 포함할지는 고려하지 않는다.

</br>지금부터는 위에서 이야기한 의존성을 각각의 버전에서 이야기 해보겠다.

한 특정 버전의 의존성은 다른 의존성의 어떤 특징 버전에서만 테스트 됐을 가능성이 있다. 따라서 라이브러리를 함께 사용하려면 특정 요건을 만족하는 엄격함이 필요하다. 특정 버전에서만 테스트된 의존성을 함께 사용할 때 문제가 생기면, 소위 말하는 **의존성 꼬임**이 발생한다.

**의존성 꼬임** 문제로 힘들었던 경험을 가지기도 한다. 의존성 불일치로 생긴 불필요한 버그를 찾아 해결하는 일은 많은 시간 소모에 비해 성과가 크지 않다.

이처럼 **스프링 부트**와 **스타터**는 이런 어려움을 해결하기 위해 등장했다. **스프링 부트 스타터**는 거의 매번 동일한 방식으로 특정 기능을 제공한다는 입증된 전제를 바탕으로 제작된 **BOM**이다. **BOM**은 프로젝트 아티팩트의 정보, 버전과 의존성 관리를 포함한 특수 **POM**이다. **POM**은 빌드 도구에서 의존성을 가져오고 프로젝트 빌드에 사용하는 정보와 프로젝트 구성이 담긴 파일이다.

앞의 예시처럼 API를 만들때마다

- 엔드포인트를 설계
- 요청을 수신해 처리
- 객체 간의 변환
- 하나 이상의 표준 형식으로 정보를 교환
- 특정 프로토콜로 데이터를 주고받는 등의 작업 수행

이러한 설계 . 개발 . 사용 패턴은 별반 다르지 않고, 큰 변경 없이 업계 전반에서 사용된다. 이런 패턴이 바로 '스프링 부트 스타터'에 반영됐다.

Spring-boot-starter-web 같은 단일 스타터를 추가하면 단일 애플리케이션에 필요한 기능을 모두 제공한다. 단일 스타터에 포함된 여러 의존성 안에 들어 있는 각 의존성 내의 여러 라이브러리 버전이 모든 의존성에 맞게 동기화된다. 즉, 모든 의존성 간의 관계가 완벽하게 테스트됐다는 말이다. 



---

### 배포 간소화 - 실행 가능한 JAR

오래전 애플리케이션 서버에 자가 애플리케이션을 배포하는 과정은 복잡했다.

##### 예를 들자면

> 오늘날 수많은 마이크로 데이터 저장소 서비스와 거의 모든 모놀리식 서비스는 데이터베이스 액세스가 가능한 애플리케이션을 만들기 위해 가음과 같은 작업을 수행했다.
>
> - 애플리케이션 서버를 설치하고 설정한다.
> - 데이터베이스 드라이버를 설치
> - 데이터베이스 커넥션을 생성
> - 커넥션 풀 생성
> - 애플리케이션을 빌드하고 테스트
> - 애플리케이션과 애플리케이션의 의존성을 애플리케이션에 배포

이 목록에서는 시스템/가상 시스템을 설정하는 관리자가 있고 특정 시점에 이 프로세스와 독립적으로 데이터베이스를 생성했다고 가정한다.

스프링 부트는 번거로운 배포 프로세스의 많은 부분을 한 단계로 간소화했으며, 만약 독자가 단일 파일을 원하는 곳까지 복사하거나 **cf push**까지 진행한다고 고려하더라고, 두 단계로 줄일 수 있다.

스프링 부트는 **Uber JAR**의 기원은 아니지만 혁명을 일으켰다. 스프링 부트는 설계자는 애플리케이션 JAR과 모든 종속적인 JAR에서 모든 파일을 추출한 다음, 단일 JAR로 결합하는 셰이딩 방식 대신 새로운 관점으로 접근했다. 만약 의도된 형식과 전달 유형을 유지하면서 '중첩된 JAR'을 만들게 된다면 어떨까?

JAR를 셰이딩하는 대신 중첩된 JAR를 사용하면 많은 잠재적 문제가 완화된다. 그 이유는 의존성 JAR **A**와 의존성 JAR **B**가 각각 다른 버전의 라이브러리 **C**를 사용할 때 발생 가능한 버전 충돌이 없기 떄문이다. 또 소프트웨어를 재패키징하고 결합하면서 소프트웨어 간 라이선스가 달라서 발생하는 법적 문제도 제거한다. 모든 종속 JAR를 원래 형식으로 유지하면 이런 문제와 그 외 문제를 깔끔하게 피해 간다.

스프링 부트를 실행하는 JAR의 내용도 간단히 추출한다. 상황에 따라 JAR의 내용을 추출하는 이유가 몇 가지 있는데, 이 내용은 나중에 다루겠다. 여기서는 실행 가능한 JAR가 원하는 기능을 실행해준다는 사실만 기억하자.




---

### 저동설정 - 스프링 부트의 마법

스프링 부트를 처음 접한 사람이 마법이라고 부르는 **자동 설정**은 스프링 부트 개발자의 생산성을 향상시키는 가장 강력한 도구일 것이다. 스프링 부트가 널리 사용되고 반복되는 사용 사례에서 의견을 제시해 믿기 힘들 정도로 생산성을 향상시켰기 때문이다.

개발자로 오랫동안 일했다면, 특정 패턴이 자주 반복된다는 사실을 틀림없이 알아차렸을 거다. 물론 전부는 아니지만 높은 비율로 그렇다. 어쩌면 특정 설계, 개발. 활동의 80% ~ 90%를 차지할 것이다.

방금전 소프트웨어에서 특정 패턴이 반복된다고 말했다. 스프링 부트 스타터 역시 특정 패턴이 일관되므로 이런 점에서 유용하다. 또 반복 패턴이 있으므로 특정 작업에서 작성해야 할 코드가 감소화된다.

스프링 부트의 관련 프로젝트인 **스프링 데이터**를 예로 들자면, 보통 데이터베이스에 엑세스할 때마다 해당 데이터베이스에 연결해야 한다. 또 애플리케이션 작업을 완료하면 잠재적인 문제 발생을 방지하기 위해 연결을 종료해야 한다. 데이터베이스가 연결된 동안에는 단순한 읽기, 쓰기 쿼리로 데이터베이스에 수많은 작업을 요청하는데, 쿼리를 적절히 사용하기 위해선 약간의 노력이 필요하다.

이제 이 모든 것을 간소화 된다고 생각해보자. 데이터베이스를 자동으로 연결하고, 애플리케이션이 종료하면 연결도 자동으로 종료한다. 간단히 컨벤션을 따라 개발자가 최소한의 노력으로 쿼리를 자동으로 만든다. 간단한 컨벤션으로 코드를 쉽게 커스터마이제이션 해서 복잡한 맞춤형 쿼리를 효율적이고 이관되게 생성한다.

이런 식으로 코드에 접근하는 방식을 **설정보다 관습**이라고 하기도 하는데, 이 방식은 특정 규칙을 처음 접하는 경우 다소 불편하게 보이기도 한다. 그러나 이전에 유사한 기능을 구현하면서 매우 간단한 작업을 위해 수백 개의 엄청난 setup / teardown / configuration 코드를 반복적으로 작성했던 경험을 비추어보면, 이 방식은 정말 참신하다. 스프링 부트는 **설정보다 관습**이라는 정신을 추구한다. 그래서 문서화로 확립된 단순한 규칙을 따라 작업을 수행하다면, 작성해야 하는 코드가 최소화되거나 아예 없어진다.

자동 설정이 개발자에게 편리성을 제공하는 방법이 또 있다.
바로 스프링 기술을 만들고 있는 팀이 **개발자 우선 환경** 설정을 제공하는 데 노력을 집중한다는 점이다. 개발자는 수많은 설정 작업이 아니라 비즈니스 로직을 만드는 작업에 집중할 때 가장 생산적이다.

</br>

**그렇다면 스프링 부트는 어떻게 만들까 라는 생각이 든다.**

또 다른 스프링 부트 프로젝트인 **스프링 클라우드 스트림**을 예로 들자면, 개발자는 RabbitMQ나 Apache Kafka 같은 메시징 플랫폼에 연결할 때 일반적으로 해당 메시징 플랫폼에 연결하고, 사용을 위해서는 호스트 이름, 포트, 자격 증명 등의 특정 설정을 지정한다.

'개발자 우선 환경'은 **localhost, default port**등의 기본값을 지정하지 않아도 개발자가 로컬에서 작업하기 편한 기본값을 제공한다. 이는 로컬 개발 환경에서는 거의 100% 일관성이 있기 때문에 의미 있는 의견이다. 하지만 프로덕션 환경에서는 그렇지 않다. 프로덕션 환경에서는 플랫폼과 호스팅 환경이 매우 다양해서 구체적인 값을 제공해야 한다.

기본값을 쓰는 공유 프로젝트는 프로젝트 설정 시 기본값을 사용하므로 개발 환경을 설정하는 시간을 많이 절약한다.

사용 사례가 80 ~ 90%의 일반적인 범주에 들지 않고, 드물지만 유용한 10 ~ 20% 범주에 속하기도 한다. 이 경우 자동 설정을 선택적으로 오버라이딩하거나 완전히 사용하지 안ㄹ도록 설정 할 수도 있지만, 그러면 스프링 부트의 잠정이 소멸된다.

**특정 의견**의 오버라이딩은 일반적으로 하나 이상의 속성을 원하는 대로 설정하거나, 스프링 부트가 사용자를 대신해 자동 설정 작업을 하는 Bean을 제공하는 경우레 수행한다. 다시 말해, 드물지만 필요할 때는 이런 작업을 매우 쉽게 할 수 있다. 결국 **자동 설정** 기능은 사용자으이 삶을 극적으로 생산적이고 더할 수 없이 편리하게 만들기 위해 뒤에서 묵묵히 쉬지 않고 작동하는 도구이다.



---

### 마치며

스프링 부트의 세 가지 핵심 기능은 **의존성 관리 간소화, 배포 간소화, 자동 설정**이다.
세 가지 기능은 모두 커스터마이징이 가능하지만, 그렇게 할 필요는 거의 없다. 그리고 세 기능은 개발자를 더욱 더 유능하고 생성적으로 만들기 위해 열심히 수행한다.