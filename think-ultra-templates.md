# Think Ultra 프롬프트 템플릿

## 개요
Sequential Thinking MCP 도구에 Think Ultra 기법을 적용하기 위한 프롬프트 템플릿 모음입니다.

## 1. Serial Test-Time Compute 템플릿

### 깊이 있는 순차 추론 템플릿
```markdown
thought: "[깊이 1/10] 문제 정의 및 범위 파악
- 핵심 요구사항: [명시]
- 제약 조건: [나열]
- 성공 기준: [정의]"
thoughtNumber: 1
totalThoughts: 25
nextThoughtNeeded: true

thought: "[깊이 2/10] 문제 분해 및 하위 과제 도출
- 주요 구성 요소: [분석]
- 의존성 관계: [매핑]
- 우선순위: [설정]"
thoughtNumber: 2
totalThoughts: 25
nextThoughtNeeded: true

thought: "[깊이 3/10] 각 하위 과제별 접근 전략
- 기술적 접근법: [검토]
- 리스크 요인: [식별]
- 대안 준비: [수립]"
thoughtNumber: 3
totalThoughts: 25
nextThoughtNeeded: true
```

### 점진적 심화 템플릿
```markdown
thought: "[표면 분석] 문제의 명백한 측면 검토..."
thought: "[심층 분석] 숨겨진 복잡성과 함의 탐구..."
thought: "[핵심 통찰] 근본적인 패턴과 원리 발견..."
```

## 2. Parallel Test-Time Compute 템플릿

### 다중 경로 탐색 템플릿
```markdown
# 메인 분기점
thought: "[분기점] 3가지 접근 방법을 병렬로 탐색하겠다"
thoughtNumber: 5
totalThoughts: 30

# 경로 A
branch_from_thought: 5
branch_id: "technical_solution"
thought: "[병렬 A - 기술적 해결책] 
- 아키텍처: 마이크로서비스
- 기술 스택: Node.js + PostgreSQL
- 확장성: 수평적 확장 전략"

# 경로 B  
branch_from_thought: 5
branch_id: "business_solution"
thought: "[병렬 B - 비즈니스 해결책]
- 프로세스 개선: 자동화 우선
- 조직 변화: 애자일 전환
- ROI 분석: 6개월 내 수익 전환"

# 경로 C
branch_from_thought: 5  
branch_id: "hybrid_solution"
thought: "[병렬 C - 하이브리드 접근]
- 단계적 전환: 레거시 + 신규
- 리스크 완화: 점진적 마이그레이션
- 빠른 성과: MVP 우선 개발"
```

### 경쟁적 가설 검증 템플릿
```markdown
branch_id: "hypothesis_1"
thought: "[가설 1] 성능 병목은 데이터베이스 쿼리
증거: 느린 응답 시간, 높은 DB CPU
검증 방법: 쿼리 프로파일링"

branch_id: "hypothesis_2"  
thought: "[가설 2] 성능 병목은 네트워크 레이턴시
증거: 분산 시스템, 지역간 통신
검증 방법: 네트워크 추적"
```

## 3. Meta-Reasoning 템플릿

### 추론 과정 평가 템플릿
```markdown
is_revision: true
thought: "[메타 추론 - 중간 점검]
✓ 논리적 일관성: 이전 단계들이 연결되는가?
✓ 완전성: 놓친 측면이 있는가?
✓ 편향성: 특정 관점에 치우쳤는가?
✓ 실용성: 실제 적용 가능한가?

발견된 문제:
- 3단계에서 비용 측면 간과
- 5단계에서 논리 비약 존재

수정 필요 사항:
- 비용 분석 추가
- 중간 단계 보강"
thoughtNumber: 15
revises_thought: 3
```

### 품질 검증 템플릿
```markdown
thought: "[메타 - 최종 검증]
1. 해결책의 완전성
   - 모든 요구사항 충족: [체크리스트]
   - edge case 처리: [검토]

2. 구현 가능성
   - 기술적 실현성: [평가]
   - 자원 요구사항: [산정]
   
3. 지속 가능성
   - 유지보수성: [고려]
   - 확장 가능성: [계획]"
```

## 4. Self-Correction 템플릿

### 오류 감지 및 수정 템플릿
```markdown
is_revision: true
revises_thought: 7
thought: "[자기 수정] 7단계에서 잘못된 가정 발견
오류: 단일 서버로 충분하다고 가정
원인: 트래픽 예측 과소평가
수정: 로드 밸런싱과 다중 서버 구성 필요

새로운 접근:
- 최소 3대 서버 구성
- 로드 밸런서 도입
- 자동 스케일링 설정"
```

### 백트래킹 템플릿
```markdown
is_revision: true
revises_thought: 10
thought: "[백트래킹] 현재 경로가 막다른 길
문제: 선택한 기술 스택의 한계 도달
대안: 3단계로 돌아가 다른 접근 시도

새로운 방향:
- 이벤트 드리븐 아키텍처
- 비동기 처리 중심
- 메시지 큐 활용"
```

## 5. Budget-Forcing Method 템플릿

### 토큰 예산 관리 템플릿
```markdown
thought: "[예산 체크] 현재 진행 상황
- 사용된 단계: 12/25
- 남은 예산: 13단계
- 효율성 모드: balanced

남은 작업 우선순위:
1. 핵심 해결책 구체화 (3단계)
2. 구현 계획 수립 (5단계)
3. 검증 및 최적화 (5단계)"
```

### 효율적 사고 템플릿
```markdown
thought: "[효율 모드 - 핵심만]
문제: X
해결: Y 방법 적용
이유: Z 때문
다음: 구현 단계"
```

## 6. Domain-Specific 템플릿

### 아키텍처 설계 전문 템플릿
```markdown
thought: "[아키텍처 - 요구사항 분석]
- 기능적 요구사항: [명세]
- 비기능적 요구사항: [품질 속성]
- 제약사항: [기술/비즈니스]"

thought: "[아키텍처 - 패턴 선택]
- 후보 패턴: [나열 및 평가]
- 선택 근거: [trade-off 분석]
- 적용 전략: [단계별 계획]"
```

### 디버깅 전문 템플릿
```markdown
thought: "[디버그 - 증상 수집]
- 에러 메시지: [전체 내용]
- 발생 조건: [재현 시나리오]
- 환경 정보: [시스템/버전]"

thought: "[디버그 - 가설 수립]
- 가능한 원인: [우선순위별]
- 검증 방법: [각 가설별]
- 필요 도구: [디버거/프로파일러]"
```

### 창의적 문제해결 템플릿
```markdown
thought: "[창의 - 발산적 사고]
- 기존 틀 벗어나기: [관점 전환]
- 유사 분야 벤치마킹: [타 산업 사례]
- 와일드 아이디어: [제약 없는 상상]"

thought: "[창의 - 수렴적 사고]
- 실현 가능성 평가: [각 아이디어]
- 조합과 융합: [시너지 창출]
- 최종 선택: [혁신성 + 실용성]"
```

## 사용 가이드

### 1. 문제 복잡도에 따른 템플릿 선택
- **단순 문제**: 효율적 사고 템플릿
- **중간 복잡도**: Serial + Self-Correction
- **고복잡도**: 모든 템플릿 조합 사용

### 2. totalThoughts 설정 가이드
- **단순**: 5-10
- **보통**: 15-20
- **복잡**: 25-30
- **매우 복잡**: 30-40

### 3. 병렬 경로 사용 시점
- 여러 해결책이 가능한 경우
- 불확실성이 높은 경우
- 창의적 접근이 필요한 경우

### 4. 메타 추론 삽입 시점
- 전체의 1/3 지점
- 전체의 2/3 지점
- 최종 단계 직전

### 5. 자기 수정 트리거
- 논리적 모순 발견
- 새로운 정보 입력
- 막다른 길 도달
- 더 나은 방법 발견