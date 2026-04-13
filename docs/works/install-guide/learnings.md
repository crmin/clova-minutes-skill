# Learnings

## TL;DR

- `clova-minutes`는 `SKILL.md` 단독 파일이 아니라 `references/`를 포함한 디렉터리 단위로 설치해야 한다.
- Codex, Claude Code, OpenCode는 각자 공식 또는 공개 문서에서 `SKILL.md` 디렉터리 구조를 지원한다.
- Antigravity는 프로젝트 로컬 `.agent/skills/<name>/`와 전역 `~/.gemini/antigravity/skills/...` 관례를 사용한다.
- 설치 안내 정책은 전역 설치를 기본으로 두고, 프로젝트 로컬은 명시적 요청이 있을 때만 열어 두는 편이 혼선을 줄인다.
- 공개 배포용 설치 문서는 한국어 응답 원칙과 별도로 영어로 두는 편이 에이전트 간 재사용성이 높다.

## 근거

- `SKILL.md` 본문이 `references/clova-note-format.md`, `references/verifiable-timestamps.md`, `references/request-examples.md`를 직접 참조함.
- Codex 공개 문서는 `.agents/skills` 계열 경로를 안내함.
- Claude Code 공개 문서는 `.claude/skills/<skill-name>/SKILL.md`를 안내함.
- OpenCode 공개 문서는 `.opencode/skills`, `.claude/skills`, `.agents/skills` 호환 경로를 안내함.
- Antigravity skill 카탈로그 예시들은 프로젝트 로컬 `.agent/skills/<name>/`와 전역 `~/.gemini/antigravity/skills/<owner>/<repo>/<skill>/SKILL.md`를 반복적으로 사용함.

## 결론

- `INSTALL.md`는 단일 파일 복사가 아니라 스킬 폴더 설치 문서로 써야 한다.
- Claude Code는 `.claude/agents/`가 아니라 `.claude/skills/` 기준으로 설명하는 편이 이 저장소 배포 형식과 맞다.
- Codex는 공개 문서 기준 경로를 우선 쓰고, 일부 환경의 `~/.codex/skills` 관행은 호환 메모로만 남기는 것이 안전하다.
- 기본 설치 정책을 전역 기준으로 통일하면 에이전트별 안내 문구를 더 단순하게 유지할 수 있다.

## 재사용 키워드

- codex skills
- claude code skills
- opencode skills
- antigravity agent skills
