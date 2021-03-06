# 마이크로서비스의 소개

### 마이크로 서비스 정의
    우리는 마이크로서비스의 high-level 특성에 대해 리뷰를 해볼것 입니다. 함께 정의 하는 특성이 어떤것이 있는지 살펴보겠습니다.

    단일 목적(Single Purpose)
        한 가지 일을 하고, 잘 해야 합니다.
    
    캡슐화(Encapsulation)
        각각의 마이크로서비스는 그들만의 자체 데이터를 소유하고 있습니다. 
        전체적인 상호작용은 잘 알려진 API들을 통해서 진행됩니다. (HTTP REST는 아니지만 자주 발생) 
    
    소유권(Ownership)
        2~15명으로 구성된 단일 팀(7명, 플러스 또는 마이너스 2명)의 사용자가 라이프 사이클 전체에 걸쳐 단일 마이크로 서비스를 개발, 구축 및 관리합니다.

    자율성(Autonomy)
        각각의 팀은 어떠한 이유를 위해 언제든지 협업없이 그들의 마이크로서비스를 개발하고 구축하는것이 가능합니다.
        각각의 팀은 또한 자체적인 구현 결정을 내리는데 있어 자유롭습니다.

    다수의 버전(Multiple versions)
        각 마이크로서비스의 다양한 버전은 같은 환경에서 동시에 존재할 수 있습니다.

    연출(Choreography)
        다수의 마이크로서비스에 걸친 작업은 분산된 방식으로 관리되며, 
        각 end-point는 해당 입출력을 충분하게 알 수 있을만큼 지능적입니다.
        그것들은 Top-down 방식의 workflow가 아니고 다수의 마이크로서비스의 경계에 걸쳐 트랜젝션을 관리합니다.


    궁극적인 일관성(Eventual consistency)
        일반적으로 모든 일관성을 갖게 됩니다.

        ※  마이크로서비스와 단일서비스를 비교하여 생각하는 것은 흥미롭습니다. 
            그러나 두가지 사이에는 각각의 단점이 있습니다. 
            마이크로서비스의 원칙이 맞다는 지지자는 거의 없습니다. 
            이 문서에 기술된 것은 교과서 적인 정의에 더 가깝습니다. 
            독자와 독자의 조직에 적합한 내용만 자유롭게 구현해야 합니다. 
            해당 문서를 독단적으로 진행하시면 안됩니다.

    이제 각각 더 깊이 알아보겠습니다.

#### 단일 목적(Single purpose)
    
    큰 규모의 단일 어플리케이션은 수천만 줄의 코드로 이루어져있고 그리고 수백개의 비즈니스 기능들로 구성되어 있습니다. 
    예를들어, 한개의 어플리케이션은 상품 관리, 재고, 가격, 프로모션, 쇼핑카트, 주문, 프로파일들 등등을 포함하고 있습니다. 
    반면에 마이크로서비스는 한가지 비즈니스 기능으로 구성되어 있습니다.
    '한 가지 일을 하고 그 일을 잘하자'라는 Unix의 기본 원칙으로 돌아가보면, 마이크로서비스는 이러한 원칙을 정의하고 있습니다. 
    한 가지 일을 잘 하면 팀이 집중 할 수 있고, 복잡성은 최소한으로 줄일 수 있습니다.

    시간이 지날수록 어플리케이션이 점점 추가되고 많은 기능이 생기는 것은 자연스러운 현상입니다.


## 마이크로서비스의 이점(Advantages of Microservices)
    마이크로서비스는 많은 이점을 제공합니다. 그 중 몇개를 구체적으로 짚어보겠습니다.

### 출시기간 단축
    새로운 특징들의 출시기간 단축은 마이크로서비스의 가장 중요한 이점입니다. 초기에 시장에 진입하는 전체적인 시간은 마이크로서비스로 도입된 부가적인 선행 복잡성 때문에 더 길어질 수 있습니다. 하지만 도입되고 난 이후에는, 각 팀은 독립적으로 혁신하고 매우 빠르게 출시할 수 있습니다.(자료 2-13)

    자료 2-13 각 팀은 독립적으로 혁신할 수 있습니다.

    시장에 빠르게 진입할 수 있는 특징을 갖는 것은 사업에서 상당히 중요한 이점을 가질 수 있습니다. 만약 출시를 위한 생산이 분기별로 이뤄지고 올바르게 바로잡기 위해 4번의 반복이 필요하다면, 결국 바로 잡는데에 1년의 시간이 소요됩니다. 만약 출시가 매일 이뤄지고 바로잡기 위해 4번의 반복이 필요하다면, 단 4일이 소요됩니다.빠른 반복뿐 아니라, 마이크로서비스는 실패를 더 빠르게 발생시킬 수 있습니다. 때때로, 특징들은 예상대로 작용하지 않습니다. 출시 취소되기까지 한 분기를 기다리는 것 보다 즉시 취소할 수 있는 것이 낫습니다.

    마이크로서비스는 의존도를 제거하기 때문에 빠릅니다. 마이크로서비스로 다음과 같은 사항을 고려할 필요가 없습니다.
    - 일원화된 구조 검토 위원회로부터의 구조적 승인
    - 경영위원으로부터 출시 승인
    - 수평적 의존성-예를들어, 공유된 DB수정을 위해 DBA를 기다릴 필요가 없고, 공급산출을 위해 영업활동이 필요가 없음
    - 수직적으로 의존적인 다른팀과 출시를 조정하는 것 - 예를들어, 재고 마이크로서비스는 상품 마이크로서비스 팀과 나란히 출시할 필요가 없을 것입니다.
    - 이러한 기능을 수행하는 QA, 보안팀 등 각 팀의 승인

    이러한 일원화된 기능을 위한 책임은 자급자족하도록 기술을 갖고 있는 각각의 작은 팀에게 전가됩니다. 각 팀은 단순히 input(보통 이벤트나 API호출) 과 output(보통 이벤트나 API들)만 상관하게 됩니다. 의존성을 제거하는 것은 개발 속도를 급격하게 증가시킵니다.

### 진정한 옴니채널 커머스
    완전하게 마이크로서비스를 도입하는 것은 각 API에 

    마이크로서비스는 의존도를 제거하기 때문에 빠릅니다. 마이크로서비스로 다음과 같은 사항을 고려할 필요가 없습니다.
    - 일원화된 구조 검토 위원회로부터의 구조적 승인
    - 경영위원으로부터 출시 승인
    - 수평적 의존성-예를들어, 공유된 DB수정을 위해 DBA를 기다릴 필요가 없고, 공급산출을 위해 영업활동이 필요가 없음
    - 수직적으로 의존적인 다른팀과 출시를 조정하는 것 - 예를들어, 재고 마이크로서비스는 상품 마이크로서비스 팀과 나란히 출시할 필요가 없을 것입니다.
    - 각 팀이 이러한 기능을 수행하는 QA, 보안팀 등등의 승인

    이러한 일원화된 기능을 위한 책임감은 각각의 작은 팀에게 강요됩니다 결국 각 팀에게 자급자족하도록 기술을 요구합니다.

## 마이크로서비스의 단점(Disadvantages of Microservices)
    비록 마이크로서비스가 확실히 장점을 가지고 있지만, 이와 마찬가지로 단점 또한 가지고 있습니다.
    마이크로서비스의 목표는 새로운 기능의 제공 속도를 높이는데 있습니다. 비용을 줄이는 것이 아닙니다.
    새로운 기능을 신속하게 출시하는 것은 추 후 잠재적인 높은 마이크로서비스 개발비용을 상쇄하게 될 것입니다.

### 외부 복잡성의 어려움
    마이크로서비스는 종종 외부 복잡성을 위해 내부를 희생시키는것으로 여겨집니다.
    단일 어플리케이션은 내부가 복잡하지만 마이크로서비스의 내부는 간단합니다.
    단일 어플리케이션의 외부 복잡성은 단순한 반면에 마이크로서비스의 외부 복잡성은 까다롭습니다.
    이러한 차이를 통해 마이크로서비스팀은 새로운 기능을 매우 빠르게 구축하고 배치 할 수 있습니다.
    하지만, 마이크로서비스간의 상호작용을 관리하는 비용을 수반합니다.

    마이크로서비스의 외부 복잡성에 대한 예시를 소개하겠습니다.
        데이터 동기화
            동기식 또는 비동기식 으로 마이크로서비스간 데이터 복사가 필요합니다.

        보안
            누가/어떤것이 End Point를 호출할 것인가요? 검색할 수 있는 데이터는 무엇인가요? 어떤 동작만을 허용할 것인가요?

        정보 찾기
            어떤 마이크로서비스가 사용가능한가요? 특정한 마이크로서비스에서 사용되는 메시지를 어떤것인가요?

        버전 관리
            특정한 API나 특정 API 구현 버전을 어떻게 관리할 것인가요?

        데이터 정확성
            어떤 마이크로서비스가 주어진 데이터를 실제로 기록할 진짜 시스템인가요?

    디버깅은 더 어렵습니다. 13.2버전 쇼핑카트 마이크로서비스와 19.1버전의 재고 관리 마이크로서비스가 서로 연관되어 있다면 어떻게 할까요?
    언제든지 동시에 다양한 버전의 마이크로서비스들이 동일한 환경에 존재하는 것을 기억해야 합니다. 
    이러한 사항으로 모든 상관관계를 테스트 하는 것은 불가합니다.
    그리고 마이크로서비스의 모든 상호작용에 대한 테스트를 중앙에서 관리하는 것은 마이크로서비스 사상에 반하는 것입니다.

### 조직 성숙도(Organizational Maturity)
    조직은 탄탄한 구조와, 문화 그리고 기술적 역량을 가지고 있어야 합니다. 각각 하나씩 살펴보겠습니다.

    우리가 이미 살펴본 것 처럼, 조직의 구조가 '소프트웨어 생성을 어떻게 해야하는가'를 정합니다.
    계층을 중심으로 하는 중앙화 된 조직은 계층화 된 단일 어플리케이션 생성을 지향합니다.
    단순한 변경일 지라도 계층 전체에 광범위한 조정이 필요하기 때문에 시간이 더 소요됩니다.
    마이크로서비스를 만들기를 원하는 조직을 위한 더 나은 구조는 재품을 재구성 하는 것 입니다.
