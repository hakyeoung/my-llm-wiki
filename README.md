# my-llm-wiki

나만의 llm 위키 레포지토리

## 구조

- `projects/`: 특정 프로젝트 맥락에서 얻은 인사이트
- `topics/`: 여러 프로젝트에 재사용할 수 있는 판단 기준과 설계 원칙

## 프로젝트

- [PlaNU](projects/planu/README.md): 부산대학교 1학년 학생의 수강신청을 돕는 프로젝트에서 얻은 LLM, Agent, 규칙 기반 설계 판단
- [FOMOdoro](projects/kakao-tech-campus/README.md): 초보 투자자에게 종목 변동 요인을 설명하는 보고서 자동 생성. 프롬프트 A/B 검증, 자료 범위 설계, 2단 검수 체계

## Topics

- [Agent를 언제 사용할 것인가](topics/agent/when-to-use-agent.md)
- [LLM과 결정론적 로직의 역할 분리](topics/llm/llm-vs-deterministic-logic.md)
- [Structured output 검증과 schema 설계](topics/llm/structured-output-validation.md)
- [프롬프트를 언제, 무엇을 근거로 고칠 것인가](topics/llm/evaluating-prompt-changes.md)
- [컨텍스트에 무엇을 넣을 것인가](topics/llm/context-scoping.md)
- [결정론적 규칙을 데이터로 분리하기](topics/backend/rules-as-data.md)
