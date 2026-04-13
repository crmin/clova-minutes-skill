# Decisions

## Current (Active)

- `README.md`는 사람 대상 소개 문서로 작성하고, 상세 설치는 `INSTALL.md`, 실행 규칙은 `SKILL.md`로 분리한다.
- `README.md`는 한국어로 작성한다.
- README 상단에는 사람이 에이전트에게 그대로 전달할 영문 설치 요청 문구를 둔다.
- README에는 결과물의 공통 구조와 특성을 직접 설명해 빠르게 파악할 수 있게 한다.
- README는 `.gitignore` 대상 파일이나 디렉터리에 의존하지 않는다.

## Change Log

### 2026-04-14

- Changed: `README.md`를 신규 작성하고 문서 역할을 소개, 설치, 명세로 분리했다.
- Reason: 사용자는 사람이 읽는 문서로서의 README를 원했고, 기존 영문 설치 문서와 영문 스킬 본문만으로는 저장소의 용도를 빠르게 파악하기 어려웠다.

### 2026-04-14

- Changed: README 상단에 `INSTALL.md` URL을 포함한 복붙용 설치 요청 문구를 추가하고, 사람이 `INSTALL.md`를 직접 읽으라고 안내하던 문구를 제거했다.
- Reason: README는 사람이 다음 행동을 빠르게 결정하게 해야 하며, 설치 문서 자체는 에이전트가 읽는 것이 더 적절하다.

### 2026-04-14

- Changed: README 상단의 설치 요청 코드블록을 영어로 수정했다.
- Reason: README는 한국어 문서이지만, 에이전트에게 직접 전달할 입력은 영어로 유지하는 것이 기존 설치 문서와 목적에 맞다.

### 2026-04-14

- Changed: README에서 `tests/` 링크와 `tests/` 디렉터리 표기를 제거했다.
- Reason: `tests/`는 `.gitignore` 대상이라 배포본에 포함되지 않을 수 있으므로 README가 해당 자산에 의존하면 안 된다.
