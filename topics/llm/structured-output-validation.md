# Structured output 검증과 schema 설계

## 현재 판단

LLM structured output은 출력 형태를 안정화하는 데 도움이 된다. 다만 schema validator가 구조 검증, 의미 검증, 실제 데이터 존재 여부 검증을 모두 떠맡으면 시스템이 지나치게 경직될 수 있다.

Pydantic 같은 schema validator는 구조와 기본적인 타입 검증에 집중시키고, 의미적 유효성은 별도의 로직에서 처리하는 편이 더 유연할 수 있다.

## 검증을 나누기

PlaNU에서 필요하다고 느낀 검증 구분:

- 구조 검증: 필드가 존재하는지, 타입이 맞는지 확인한다.
- 의미 검증: 값이 사용자 의도와 일치하는지 확인한다.
- 데이터 존재 여부 검증: 추출된 값이 실제 후보 데이터에 존재하는지 확인한다.

자연어에서 추출된 값을 정확한 DB 값에 바로 매핑하도록 강제하면, 의미상 맞는 값을 validator가 거부할 수 있다. 중간에 후보 데이터와 매칭하거나 보정하는 단계가 필요할 수 있다.

## Schema는 단순하고 겹치지 않게 유지한다

LLM이 변환해야 하는 schema는 가능한 한 의미가 겹치지 않아야 한다.

PlaNU에서는 다음 필드처럼 비슷한 의미를 가진 조건들이 동시에 존재하면 LLM이 어느 필드에 값을 넣어야 하는지 혼란을 줄 수 있다고 판단했다.

- `earliest_start_time`
- `no_morning_classes`
- `morning_end_time`

현재 판단: 하나의 개념은 하나의 필드로 표현하는 것이 좋다. 조건 종류를 세분화할수록 LLM의 분류 부담과 후처리 복잡도가 커질 수 있다.

## Fallback 설계

LLM 시스템에서는 실패 가능성을 없애려 하기보다, 실패했을 때 결정론적인 fallback 경로를 마련하는 것이 더 현실적이다.

PlaNU에서 고려한 흐름:

- LLM 추출 성공: 바로 진행
- LLM 추출 실패: 파싱된 과목 목록을 사용자에게 보여주고 직접 선택하게 한다

prompt와 validator를 계속 강화하는 것만으로 모든 실패를 막으려 하면, 검증이 지나치게 엄격해져 다른 정상 입력까지 거부할 수 있다.

## 근거

- [PlaNU Lessons](../../projects/planu/lessons.md)
- [PlaNU Decisions](../../projects/planu/decisions.md)

## 검증 상태

이 문서는 PlaNU에서 관찰한 패턴을 바탕으로 한 현재 판단이다. 다른 LLM 애플리케이션에서도 반복 확인되면 `schema-design-for-llm.md`나 `fallback-design.md`로 분리할 수 있다.
