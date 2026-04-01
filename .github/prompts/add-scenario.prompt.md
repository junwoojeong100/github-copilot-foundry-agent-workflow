---
description: "새로운 AI 에이전트 시나리오를 추가합니다"
mode: "agent"
---

<!-- 🔒 프로젝트 전용: 이 프로젝트의 RAG/MCP/멀티에이전트 시나리오 구조에 특화되어 있습니다. -->

# 새 에이전트 시나리오 추가

## 요청사항

아래 시나리오에 맞는 새 에이전트를 만들어주세요.

- 에이전트명: {{agent_name}}
- 역할: {{role_description}}
- 유형: RAG / MCP 도구 / 멀티 에이전트
- 필요한 도구: {{tools}}

## 현재 시나리오 구조

1. **RAG 에이전트** (`create_rag_agent`) — Foundry IQ(Knowledge Base) 기반 문서 검색
2. **MCP 도구 에이전트** (`create_tool_agent`) — MCPStdioTool → mcp_server.py
3. **멀티 에이전트** (`create_workflow_agent`) — WorkflowBuilder + Switch 라우팅 (RAG / TOOL / BOTH 순차 파이프라인)

## 규칙

- `demo/app.py`의 기존 에이전트 생성 패턴을 따를 것:
  ```python
  # 단일 에이전트: @st.cache_resource로 캐시 가능
  @st.cache_resource
  def create_xxx_agent():
      return Agent(
          client=get_ai_client(),
          name="...",
          instructions="...",
          tools=[mcp_tool],              # MCP: MCPStdioTool
          context_providers=[kb_provider], # RAG: AzureAISearchContextProvider
      )

  # WorkflowAgent: 캐시 금지 (내부 실행 상태 추적으로 동시 실행 충돌)
  def create_workflow_xxx_agent():
      ...
      return WorkflowAgent(workflow=workflow, name="...", description="...")
  ```
- RAG 도구 추가: `AzureAISearchContextProvider`를 `context_providers`로 전달
- MCP 도구 추가: `demo/mcp_server.py`에 `@server.tool()` 추가 → MCPStdioTool이 자동 로드
- 멀티 에이전트: `WorkflowBuilder` + `AgentExecutor` + `Case`/`Default`로 구성, BOTH 경로는 `add_chain`으로 순차 파이프라인
- 스트리밍: `stream_agent()` 함수로 `st.write_stream()` 연동 (토큰 단위 실시간 출력)
- instructions에 역할, 사용 가능 도구, 가이드라인을 한국어로 명시
- 사이드바 radio 선택지에 새 시나리오 추가
