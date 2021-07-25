# MSA ( Micro Service Architecture )
하나의 큰 어플리케이션을 여러개의 작은 어플리케이션으로 쪼개 변경과 조합이 가능하도록 만든 아키텍쳐 like 레고

## Monolithic Architecture vs Microservices
**Monolithic Architecture란?**
 - 소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어있는 형태
 - 소규모 프로젝트에 적합. 간단하고 유지보수가 용이하다

단점
- 서비스가 커질수록 구조파악이 어렵다.
- 빌드, 테스트, 배포시간이 늘어난다
- 부분의 장애가 전체 서비스의 장애로 이어진다.

**MSA란?**

장점 
- 비즈니스 민첩성(Business agility)와 관련있다.
- 서비스가 클수록 장점이 드러난다
- 배포(deployment) : 서비스 별 개별 배포가 가능하다. 요구사항의 신속한 반영이 가능하다
- 확장(scaling) : 서비스에 대한 확장성이 좋다. 클라우드 사용에 적합하다.
- 장애(failure) : 장애가 전체 서비스로 확장될 가능성이 적다.

단점
 - 복잡하고 서비스가 커질수록 복잡도가 늘어날 수 있다.
 - 성능 : 서비스 간 호출시 API를 사용하기 때문에 통신 비용이나 latency가 늘어난다
 - 테스트 / 트랜잭션 : 서비스가 분리되어있어 테스트와 트랜잭션의 복잡도가 증가.
 - 데이터 관리 데이터가 분산되기 때문에 정합성 관리하기 어렵다.



### 참조
[MSA란?](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1-MSA%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-3sk28yrv0e)<br>
[MSA 개념소개](http://clipsoft.co.kr/wp/blog/%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98msa-%EA%B0%9C%EB%85%90/)<br>
