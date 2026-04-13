# install-guide 계획

## 목표

- `install.draft.md`를 바탕으로 공개 배포용 `INSTALL.md`를 작성한다.
- Codex, Claude Code, Antigravity, OpenCode별 설치 경로와 설치 지침을 포함한다.
- 전역 설치를 기본으로 하고, 사용자 요청이 있을 때만 프로젝트 로컬 설치를 안내한다.
- 최종 `INSTALL.md` 본문은 GitHub 배포용으로 영어로 작성한다.
- 에이전트별 설치 문서만 보고도 설치를 진행할 수 있게 작성한다.

## 범위

- `INSTALL.md` 신규 작성
- 설치 경로 조사 결과를 `docs/works/install-guide/`에 기록

## Out of scope

- `README.md` 신규 작성
- 실제 원격 저장소 생성
- 설치 자동화 스크립트 추가

## TODO

- [x] 초안 요구사항 확인
- [x] 에이전트별 스킬 설치 경로 조사
- [x] `INSTALL.md` 작성
- [x] 최종 문구 점검

## 리스크와 가정

- Codex는 공개 문서 경로와 일부 로컬 도구 경로가 다를 수 있다.
- Claude Code는 네이티브 서브에이전트와 skill 패키지 경로가 다르므로 혼동 가능성이 있다.
- Antigravity 전역 경로는 Agent Skills 카탈로그 관례를 따른다.

## 완료 기준

- `INSTALL.md`만 보고 각 에이전트가 설치 위치를 결정할 수 있다.
- `SKILL.md`와 `references/`를 함께 복사해야 한다는 점이 명확하다.
- `INSTALL.md`가 설치 절차만 담는 문서로 정리되어 있다.
- 전역 설치가 기본이라는 정책이 문서 전반에 일관되게 반영되어 있다.
