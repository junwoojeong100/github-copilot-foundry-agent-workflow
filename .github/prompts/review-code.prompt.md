---
description: "코드를 리뷰하고 개선사항을 제안합니다"
mode: "agent"
---

<!-- 🔒 프로젝트 전용: 리뷰 체크리스트가 이 프로젝트의 Agent Framework 패턴에 특화되어 있습니다. -->

# 코드 리뷰 요청

## 대상

{{file_or_feature}} 코드를 리뷰해주세요.

## 체크리스트

아래 관점에서 검토하고 개선사항을 한국어로 알려주세요:

1. **에러 처리** — 예외 상황이 적절히 처리되는가?
2. **보안** — 환경변수 노출, 입력값 검증 누락은 없는가?
3. **성능** — 불필요한 API 호출이나 중복 연산은 없는가?
4. **패턴 준수** — `AzureAIAgentClient` + `Agent` + `tools`/`context_providers` 패턴을 따르는가?
5. **한국어 품질** — docstring, 주석, 사용자 메시지가 자연스러운가?
6. **RAG/MCP 정합성** — RAG는 `AzureAISearchContextProvider`를 `context_providers`로 사용하고, MCP 도구는 `mcp_server.py`에 있는가?
7. **멀티 에이전트 정합성** — WorkflowBuilder 라우팅과 서브 에이전트 도구 구성이 올바른가? BOTH 경로의 순차 파이프라인(RAG → Tool → Summarizer)이 정상 동작하는가? `WorkflowAgent`에 `@st.cache_resource`가 적용되어 있지 않은가? (적용 시 동시 실행 충돌)
8. **스트리밍** — `stream_agent()` + `st.write_stream()` 패턴을 사용하는가? 비동기 스트림이 `queue.Queue`로 올바르게 변환되는가?

## 출력 형식

```
### ✅ 잘된 점
- ...

### ⚠️ 개선 제안
- [파일:줄번호] 설명

### 🔴 반드시 수정
- [파일:줄번호] 설명
```
