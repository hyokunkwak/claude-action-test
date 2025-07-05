# Think Ultra 도메인별 사용 예제

## 1. 소프트웨어 아키텍처 설계

### 시나리오: 대규모 이커머스 플랫폼 마이그레이션

#### Phase 1: Serial Deep Analysis
```markdown
thought: "[깊이 1/10] 현재 시스템 분석
- 모놀리식 아키텍처: PHP + MySQL
- 일일 사용자: 50만명
- 피크 시간 TPS: 10,000
- 주요 문제: 확장성 한계, 배포 복잡도"
thoughtNumber: 1
totalThoughts: 30

thought: "[깊이 2/10] 마이그레이션 목표 정의
- 목표 아키텍처: 마이크로서비스
- 성능 목표: TPS 50,000 지원
- 무중단 전환 필수
- 점진적 마이그레이션 전략"
thoughtNumber: 2

thought: "[깊이 3/10] 핵심 도메인 식별
- 주문 관리 (Order Service)
- 상품 카탈로그 (Product Service)
- 사용자 인증 (Auth Service)
- 결제 처리 (Payment Service)
- 재고 관리 (Inventory Service)"
thoughtNumber: 3
```

#### Phase 2: Parallel Architecture Exploration
```markdown
branch_from_thought: 3
branch_id: "microservices_pure"
thought: "[병렬 A - 순수 마이크로서비스]
- 각 서비스 독립 DB
- API Gateway 패턴
- 서비스 메시: Istio
- 컨테이너: Kubernetes
장점: 완전한 독립성, 확장성
단점: 복잡도 높음, 분산 트랜잭션"

branch_from_thought: 3
branch_id: "modular_monolith"
thought: "[병렬 B - 모듈형 모놀리스]
- 도메인별 모듈 분리
- 공유 DB, 논리적 분리
- 점진적 분리 가능
- 배포는 단일 단위
장점: 단순함, 트랜잭션 보장
단점: 확장성 제한"

branch_from_thought: 3
branch_id: "hybrid_approach"
thought: "[병렬 C - 하이브리드 접근]
- 핵심 서비스만 분리
- 나머지는 모놀리스 유지
- Event Sourcing 도입
- CQRS 패턴 적용
장점: 실용적, 리스크 관리
단점: 두 패러다임 공존"
```

#### Phase 3: Meta-Reasoning
```markdown
is_revision: true
thought: "[메타 추론 - 아키텍처 평가]
각 접근법 종합 평가:

1. 팀 역량 분석
   - 마이크로서비스 경험: 제한적
   - DevOps 성숙도: 중간
   - 도메인 지식: 높음

2. 비즈니스 제약
   - 마이그레이션 기간: 6개월
   - 다운타임 허용: 0
   - 예산: 제한적

3. 기술 부채
   - 레거시 의존성 높음
   - 테스트 커버리지: 40%

결론: 하이브리드 접근이 최적"
thoughtNumber: 15
```

#### Phase 4: Implementation Strategy
```markdown
thought: "[구현 전략 - 단계별 계획]
Phase 1 (2개월): 준비 단계
- 모놀리스 리팩토링
- 도메인 경계 명확화
- 테스트 커버리지 70% 달성
- CI/CD 파이프라인 구축

Phase 2 (2개월): 첫 서비스 분리
- Auth Service 분리
- API Gateway 도입
- 모니터링 시스템 구축
- Canary 배포 전략

Phase 3 (2개월): 핵심 서비스 분리
- Order, Payment 서비스 분리
- Event Bus 구현
- Saga 패턴으로 분산 트랜잭션
- 성능 최적화"
thoughtNumber: 20
```

## 2. 복잡한 버그 디버깅

### 시나리오: 프로덕션 메모리 누수 해결

#### Phase 1: 증상 분석
```markdown
thought: "[디버그 1/8] 문제 현상 수집
- 증상: 서버 메모리 사용량 지속 증가
- 패턴: 24시간마다 OOM 발생
- 환경: Node.js 18, Express, MongoDB
- 영향: 일일 2-3회 서비스 재시작 필요"
thoughtNumber: 1
totalThoughts: 25

thought: "[디버그 2/8] 초기 데이터 수집
- Heap 스냅샷 분석 결과
- 메모리 그래프 패턴 확인
- GC 로그 검토
- APM 데이터 분석"
thoughtNumber: 2
```

#### Phase 2: 병렬 가설 검증
```markdown
branch_from_thought: 2
branch_id: "event_listener_leak"
thought: "[가설 A - 이벤트 리스너 누수]
증거: 
- EventEmitter 인스턴스 증가
- removeListener 호출 없음
검증 방법:
- 이벤트 리스너 카운트 로깅
- 생명주기 추적"

branch_from_thought: 2
branch_id: "db_connection_leak"
thought: "[가설 B - DB 연결 누수]
증거:
- MongoDB 연결 수 증가
- 연결 풀 고갈 경고
검증 방법:
- 연결 풀 모니터링
- 연결 생성/해제 로깅"

branch_from_thought: 2
branch_id: "closure_reference"
thought: "[가설 C - 클로저 참조 문제]
증거:
- 특정 API 호출 후 메모리 증가
- 대용량 객체 참조 유지
검증 방법:
- 메모리 프로파일링
- 참조 체인 분석"
```

#### Phase 3: 깊이 있는 분석
```markdown
thought: "[디버그 심화] 가설 C 검증 결과
발견: WebSocket 핸들러의 클로저 문제
- 각 연결마다 전체 user 객체 캡처
- 연결 해제 시 참조 유지
- 가비지 컬렉션 불가

코드 위치: 
/src/websocket/handler.js:45-67"
thoughtNumber: 10

is_revision: true
revises_thought: 10
thought: "[수정된 분석] 추가 발견사항
- 문제가 WebSocket뿐 아니라 
- Redis 구독 핸들러에서도 발생
- 동일한 패턴의 메모리 누수

영향 범위 확대됨"
thoughtNumber: 11
```

#### Phase 4: 해결책 구현
```markdown
thought: "[해결책] 메모리 누수 수정 전략
1. WebSocket 핸들러 리팩토링
   - WeakMap으로 참조 관리
   - 명시적 cleanup 함수

2. Redis 구독 관리 개선
   - unsubscribe 로직 추가
   - 연결 풀 크기 제한

3. 전역 메모리 관리
   - 주기적 GC 강제 실행
   - 메모리 임계값 모니터링

4. 테스트 추가
   - 메모리 누수 감지 테스트
   - 부하 테스트 시나리오"
thoughtNumber: 20
```

## 3. AI/ML 모델 최적화

### 시나리오: 추천 시스템 성능 개선

#### Phase 1: 현재 시스템 분석
```markdown
thought: "[ML 분석 1/10] 현재 추천 시스템 평가
- 모델: Collaborative Filtering
- 정확도: Precision@10 = 0.65
- 응답 시간: 평균 300ms
- 콜드 스타트 문제 심각"
thoughtNumber: 1
totalThoughts: 28

thought: "[ML 분석 2/10] 데이터 파이프라인 검토
- 일일 배치 학습
- 특징 벡터: 50차원
- 사용자 행동 데이터: 3개월치
- 실시간 업데이트 없음"
thoughtNumber: 2
```

#### Phase 2: 병렬 개선 방안
```markdown
branch_from_thought: 2
branch_id: "deep_learning_approach"
thought: "[병렬 A - 딥러닝 모델]
- Two-Tower 아키텍처
- BERT 기반 텍스트 임베딩
- 실시간 특징 업데이트
예상 개선: 정확도 +15%
필요 자원: GPU 클러스터"

branch_from_thought: 2
branch_id: "hybrid_model"
thought: "[병렬 B - 하이브리드 모델]
- CF + Content-based 결합
- 앙상블 접근법
- A/B 테스트로 가중치 조정
예상 개선: 정확도 +10%
필요 자원: 현재 인프라 활용"

branch_from_thought: 2
branch_id: "real_time_learning"
thought: "[병렬 C - 실시간 학습]
- Online Learning 도입
- Bandit 알고리즘
- 스트리밍 파이프라인
예상 개선: 신선도 +30%
필요 자원: 스트리밍 인프라"
```

#### Phase 3: 실험 설계
```markdown
thought: "[실험 설계] A/B 테스트 전략
그룹 분할:
- Control: 현재 모델 (20%)
- Treatment A: 딥러닝 (20%)
- Treatment B: 하이브리드 (30%)
- Treatment C: 실시간 (30%)

측정 지표:
- CTR (Click-Through Rate)
- 체류 시간
- 구매 전환율
- 시스템 레이턴시

실험 기간: 4주"
thoughtNumber: 15
```

## 4. 비즈니스 전략 수립

### 시나리오: 신규 시장 진입 전략

#### Phase 1: 시장 분석
```markdown
thought: "[전략 1/12] 목표 시장 분석
- 시장: 동남아 전자상거래
- 규모: $100B, 연 성장률 25%
- 주요 플레이어: 3개 대기업
- 진입 장벽: 물류, 결제 인프라"
thoughtNumber: 1
totalThoughts: 35
```

#### Phase 2: 병렬 전략 탐색
```markdown
branch_from_thought: 3
branch_id: "direct_entry"
thought: "[전략 A - 직접 진입]
- 현지 법인 설립
- 자체 물류망 구축
- 로컬 마케팅 팀
투자: $50M
회수 기간: 3년
리스크: 높음"

branch_from_thought: 3
branch_id: "partnership"
thought: "[전략 B - 전략적 제휴]
- 현지 기업과 JV
- 기존 인프라 활용
- 시장 지식 공유
투자: $20M
회수 기간: 2년
리스크: 중간"

branch_from_thought: 3
branch_id: "acquisition"
thought: "[전략 C - 인수합병]
- 중소 플레이어 인수
- 즉시 시장 점유
- 기존 고객 확보
투자: $80M
회수 기간: 4년
리스크: 중간"
```

#### Phase 3: Meta-Analysis
```markdown
is_revision: true
thought: "[메타 분석 - 전략 종합 평가]
SWOT 분석 결과:
- 강점: 기술력, 자본력
- 약점: 현지 경험 부족
- 기회: 급성장 시장
- 위협: 규제 불확실성

결론: 단계적 접근
1단계: 전략적 제휴로 시작
2단계: 성과 기반 지분 확대
3단계: 완전 인수 또는 독립"
thoughtNumber: 25
```

## 5. 창의적 문제 해결

### 시나리오: 혁신적인 사용자 경험 설계

#### Phase 1: 발산적 사고
```markdown
thought: "[창의 1/8] 기존 패러다임 해체
현재 UX의 한계:
- 2D 인터페이스 중심
- 클릭/터치 인터랙션
- 단방향 정보 전달

새로운 가능성:
- 공간 컴퓨팅
- 음성/제스처 인터페이스
- 양방향 AI 대화"
thoughtNumber: 1
totalThoughts: 20
```

#### Phase 2: 창의적 조합
```markdown
branch_from_thought: 3
branch_id: "spatial_commerce"
thought: "[아이디어 A - 공간 커머스]
- AR로 실제 공간에 상품 배치
- 제스처로 상품 조작
- AI 스타일리스트 홀로그램
- 소셜 쇼핑 공간"

branch_from_thought: 3
branch_id: "conversational_ui"
thought: "[아이디어 B - 대화형 UI]
- 전체 UI가 AI 에이전트
- 자연어로 모든 조작
- 컨텍스트 aware 추천
- 감정 인식 피드백"

branch_from_thought: 3
branch_id: "predictive_interface"
thought: "[아이디어 C - 예측형 인터페이스]
- 사용자 의도 선제적 파악
- 다음 행동 자동 준비
- 개인화된 워크플로우
- 제로 클릭 경험"
```

## 사용 가이드

### 1. 도메인 선택 기준
- **아키텍처**: 시스템 설계, 마이그레이션, 확장성
- **디버깅**: 버그 수정, 성능 문제, 시스템 장애
- **ML/AI**: 모델 최적화, 알고리즘 선택, 실험 설계
- **비즈니스**: 전략 수립, 시장 분석, 의사결정
- **창의성**: 혁신, UX 설계, 제품 기획

### 2. 복잡도별 접근법
- **낮음**: Serial 중심, 5-10 단계
- **중간**: Serial + Parallel, 15-20 단계
- **높음**: 전체 기법 활용, 25-35 단계

### 3. 성공 지표
- 문제 해결의 완전성
- 실행 가능성
- 혁신성과 실용성의 균형
- 리스크 관리 수준