---
description: "새로운 에이전트 도구(Tool) 함수를 생성합니다"
mode: "agent"
---

<!-- 🔒 프로젝트 전용: 이 프로젝트의 mcp_server.py 구조에 특화되어 있습니다. -->

# 새 에이전트 도구 생성

## 요청사항

새로운 도구 함수를 추가해주세요.

- 함수명: {{function_name}}
- 기능: {{description}}
- 카테고리: RAG 문서검색 / MCP 도구

## 규칙

### RAG 도구 (문서 검색)
- Foundry IQ(Knowledge Base) 연동: `AzureAISearchContextProvider`를 `context_providers`로 전달
- `demo/app.py`의 `_get_kb_context_provider()`에서 KB 구성 관리

### MCP 도구 (업무 도구)
- `demo/mcp_server.py`에 `@server.tool()` 데코레이터로 추가
- Mock 데이터는 `demo/mock_data.json`에서 로드하여 사용 (3월~12월 월별 데이터)
- MCP 서버 재시작만으로 에이전트에서 자동 사용 가능 (MCPStdioTool이 동적 로드)
- `demo/app.py` 수정 불필요

### 공통
- Google 스타일 한국어 docstring (Args 포함)
- 반환값은 사람이 읽기 쉬운 한국어 문자열
- 멀티 에이전트 워크플로우의 서브 에이전트에도 자동으로 반영됨
