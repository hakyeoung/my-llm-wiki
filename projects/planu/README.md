# PlaNU

PlaNU는 부산대학교 1학년 학생의 수강신청을 돕기 위해 진행한 프로젝트다.

초기에는 LLM이 사용자의 조건을 해석하고 시간표를 생성하는 구조를 고민했다. 진행 과정에서 결정론적 로직, 규칙 기반 처리, 백트래킹, LLM structured output, Agent 구조를 함께 실험했다.

프로젝트 후반에는 단순한 시간표 생성 앱을 Agent로 만드는 것이 적절한지 다시 검토하게 되었고, 이 과정에서 LLM과 Agent를 어떤 문제에 사용해야 하는지에 대한 현재 판단이 형성되었다.

이 프로젝트 문서는 PlaNU에서 무엇을 구현했는지보다, PlaNU를 진행하면서 어떤 기술적 판단 기준을 얻게 되었는지를 기록한다.

## 관련 문서

- [Lessons](lessons.md)
- [Decisions](decisions.md)
- [Retrospective](retrospective.md)
- [Agent를 언제 사용할 것인가](../../topics/agent/when-to-use-agent.md)
- [LLM과 결정론적 로직의 역할 분리](../../topics/llm/llm-vs-deterministic-logic.md)
- [Structured output 검증과 schema 설계](../../topics/llm/structured-output-validation.md)
- [결정론적 규칙을 데이터로 분리하기](../../topics/backend/rules-as-data.md)
