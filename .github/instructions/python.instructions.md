---
applyTo: "**/*.py"
---

<!-- 🌐 공용: 다른 프로젝트에서도 .github/instructions/에 복사하여 재사용할 수 있습니다. -->

# Python 프로젝트 공통 인스트럭션

## Python 가상환경 설정

- Python 3.12 기반 `.venv` 가상환경을 사용한다.
- 가상환경 생성 및 활성화:
  ```bash
  python3.12 -m venv .venv
  source .venv/bin/activate   # macOS / Linux
  ```
- 패키지 설치는 반드시 가상환경 활성화 후 진행한다:
  ```bash
  pip install -r requirements.txt
  ```
- `.venv/` 디렉토리는 `.gitignore`에 포함하여 버전 관리에서 제외한다.

## 의존성 관리

- 프로젝트 의존성은 `requirements.txt`에 명시한다.
- 새 패키지를 추가하면 `requirements.txt`를 갱신한다:
  ```bash
  pip freeze > requirements.txt
  ```
- 프로덕션 의존성과 개발 의존성을 분리할 경우 `requirements-dev.txt`를 별도로 관리한다.
- 버전 지정 전략:
  - 안정 릴리스가 있는 패키지는 `>=` 또는 `~=`로 최소 버전을 지정한다.
  - RC/프리릴리스 패키지는 `>=X.Y.ZrcN`으로 명시하고 `pip install --pre`로 설치한다.
  - 유틸리티 패키지(`python-dotenv` 등)는 버전 미지정도 허용하되, 재현성이 중요하면 고정한다.

## 코드 컨벤션

- 한국어 주석과 docstring을 사용한다.
- 모듈 최상단에 모듈 설명 docstring을 작성한다.
- 함수에는 Args/Returns를 포함한 Google 스타일 docstring을 작성한다.
- 타입 힌트를 적극 활용한다.
- import 순서: 표준 라이브러리 → 서드파티 → 로컬 모듈 (각 그룹 사이에 빈 줄).
