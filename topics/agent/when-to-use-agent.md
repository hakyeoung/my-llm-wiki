# Agent를 언제 사용할 것인가

## 현재 판단

Agent의 핵심 가치는 Tool 호출 자체가 아니라, 상황에 따라 다음 행동을 선택하는 데 있다.

LLM을 사용하거나 Tool을 여러 개 호출한다는 이유만으로 시스템을 Agent로 설계할 필요는 없다. 실행 순서가 거의 고정되어 있고 어떤 Tool을 사용할지도 미리 결정되어 있다면, 일반적인 workflow나 service orchestration이 더 적절할 수 있다.

## 판단 질문

Agent 도입 전에는 다음 질문을 먼저 확인한다.

1. 문제가 결정론적인 workflow로 충분히 해결 가능한가?
2. 실행 중 새로운 정보에 따라 다음 행동을 선택해야 하는가?
3. 어떤 Tool을 사용할지 사전에 고정하기 어려운가?
4. 사용자의 목표를 달성하기 위해 계획을 수정해야 하는가?
5. Agent의 추가 latency와 복잡성이 실제 사용자 가치로 이어지는가?

이 질문들에 대한 답이 대부분 부정적이라면 Agent를 도입하지 않는 것이 더 나을 수 있다.

## PlaNU에서 관찰한 패턴

PlaNU에서는 전공 과목 입력, 교양 후보 필터링, 시간 충돌 검사, 학과별 수강 가능 여부 검사, 캠퍼스 이동 가능 여부 검사, 후보 탐색, 점수 계산이 대부분 정해진 절차로 표현 가능했다.

이 경우 Agent보다 결정론적 workflow가 문제에 더 잘 맞을 수 있다고 판단했다.

## Tool 설계

Tool 수가 많아지는 것 자체보다 Tool의 책임이 겹치는 것이 더 큰 문제였다.

현재 판단:

- Tool은 "어떤 질문에 답하는가?"가 명확해야 한다.
- 하나의 Tool이 너무 많은 일을 하면 Agent가 선택하기 어렵다.
- 여러 Tool이 같은 판단을 반복하면 흐름 추적과 검증이 어려워진다.
- 먼저 Tool의 책임을 정리하고 workflow를 단순화한 뒤 Agent 필요성을 다시 판단한다.

## Reflection과 LLM-as-a-Judge

LLM이 생성한 결과를 다른 LLM이나 별도의 판단 단계로 검증하는 방식은 품질을 높일 가능성이 있다. 하지만 PlaNU에서는 LLM 판단 단계를 추가할수록 실행 시간이 길어지는 문제가 있었다.

현재 판단:

- Reflection이나 LLM-as-a-Judge를 모든 단계에 적용하는 것은 비용과 latency 측면에서 비효율적일 수 있다.
- 오류 비용이 높은 결정에만 선택적으로 적용하는 것이 낫다.
- 단순한 규칙으로 검증 가능한 내용은 코드로 검증하는 편이 낫다.
- "LLM을 하나 더 붙이면 정확도가 올라갈 것"이라는 이유만으로 검증 Agent를 추가하지 않는다.

## Multi-Agent

PlaNU에서는 Tool 수가 늘어나면서 역할별 Agent나 Sub-agent 구조를 검토했다. 그러나 LLM 호출 수 증가, latency 증가, 흐름 추적 어려움, 상태 관리 복잡성 증가, 단순한 문제까지 Agent 간 통신으로 처리하게 되는 문제가 있었다.

현재 판단:

- Tool이 많아졌다는 이유만으로 Multi-Agent 구조로 전환하지 않는다.
- 먼저 Tool 책임, workflow, 결정론적 처리 가능성을 정리한다.
- 그 뒤에도 역할 분리가 필요할 때만 Multi-Agent를 검토한다.

## 사용자 통제

Agent가 사용자의 목표를 대신 정의해서는 안 된다.

PlaNU에서는 Hard constraint를 Agent가 임의로 바꾸면 사용자 의도를 침해할 수 있다고 판단했다. Agent가 할 수 있는 일은 Soft preference의 조정 후보를 제안하고, 실제 변경 여부는 사용자에게 확인하는 수준이 더 적절할 수 있다.

## 근거

- [PlaNU Lessons](../../projects/planu/lessons.md)
- [PlaNU Decisions](../../projects/planu/decisions.md)
- [PlaNU Retrospective](../../projects/planu/retrospective.md)

## 검증 상태

이 문서는 PlaNU에서 관찰한 패턴을 바탕으로 한 현재 판단이다. 다른 프로젝트에서도 반복적으로 확인되면 더 세분화할 수 있다.
