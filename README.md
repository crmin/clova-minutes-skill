# clova-minutes

`clova-minutes`는 Clova Note 전사 텍스트와 Markdown 회의록 템플릿을 바탕으로, 근거 시각이 포함된 검증 가능한 회의록을 작성하도록 돕는 Agent Skill입니다.

## 설치

에이전트에게 아래 내용을 복사해서 그대로 요청하세요.

```text
Install the `clova-minutes` skill by following this URL: `https://github.com/crmin/clova-minutes-skill/blob/main/INSTALL.md`
```

이 스킬은 단순 요약이 아니라 다음 문제를 해결하는 데 초점을 둡니다.

- 어떤 전사 파일을 써야 하는지 애매할 때 후보를 찾아 사용자에게 선택을 요청
- 어떤 회의록 템플릿을 써야 하는지 자동으로 찾고 필요한 placeholder를 채움
- 출력 파일 경로가 파일인지 디렉터리인지 구분해 안전하게 저장
- 회의록의 각 문장이나 항목마다 근거 timestamp를 남겨 사후 검증 가능성 확보

## 무엇을 하는 스킬인가

이 스킬은 아래 세 가지 입력을 기준으로 동작합니다.

1. Clova Note 전사 파일
2. Markdown 회의록 템플릿
3. 출력 경로(선택)

사용자가 세 가지를 모두 정확히 지정하지 않아도 됩니다. 스킬은 현재 디렉터리, 다운로드 디렉터리, 문서 디렉터리, 템플릿 디렉터리 같은 후보 위치를 확인해 적절한 대상을 찾고, 모호하면 임의 추정 없이 사용자에게 선택을 요청합니다.

## 핵심 동작

- 전사 파일 경로가 없으면 현재 디렉터리의 `.txt` 파일을 확인하고, 하나만 있으면 사용합니다.
- 파일 이름만 주어지면 현재 디렉터리, `$HOME/Downloads`, Windows에서는 `$HOME/Documents`까지 탐색합니다.
- 템플릿이 없으면 `$HOME/.scribe` 아래 템플릿을 확인합니다.
- 출력 경로가 생략되면 기본 파일명 `회의록_{meeting_date}_{source_transcript_filename}.md`로 현재 디렉터리에 저장합니다.
- 출력 경로가 기존 파일이면 덮어쓰지 않고 중단합니다.
- 템플릿의 heading, list, table 구조를 유지하면서 `{placeholder}`를 실제 값으로 대체합니다.

## 왜 검증 가능한가

이 스킬은 회의록의 각 문장 또는 bullet마다 최소 하나 이상의 근거 timestamp를 남기도록 설계되어 있습니다.

예시:

```md
- 첫 모임은 4월 25일 12시로 정했다. <!--@time="12:18",@participant="participant_name"-->
```

이 규칙 덕분에 작성된 회의록을 나중에 다시 읽을 때, 어떤 발화와 시각을 근거로 요약되었는지 추적할 수 있습니다.

## 입력 형식

### 전사 파일

Clova Note plain text 파일을 전제로 합니다. 전사 파일에는 보통 다음 정보가 포함됩니다.

- 회의 제목
- 녹음 일시
- 총 길이
- 참석자 목록
- 발화자 이름
- 발화 시작 시각
- 발화 내용

자세한 형식은 [references/clova-note-format.md](./references/clova-note-format.md)를 보면 됩니다.

### 회의록 템플릿

템플릿은 Markdown 파일이며, heading, list, table, frontmatter, `{placeholder}`를 포함할 수 있습니다. 이 스킬은 템플릿 구조를 유지하면서 채울 수 있는 값은 직접 채우고, 요약이 필요한 부분은 전사 내용을 근거로 작성합니다.

### 출력 파일

기본 파일명은 아래 형식을 사용합니다.

```text
회의록_{meeting_date}_{source_transcript_filename}.md
```

`meeting_date`는 전사 파일의 `record_date`를 `YYYY-MM-DD`로 정규화한 값이고, `source_transcript_filename`은 원본 전사 파일명에서 확장자를 제거한 값입니다.

## 언제 유용한가

- Clova Note로 회의를 녹음해 두었지만, 사람이 직접 회의록을 정리하기에는 시간이 아까울 때
- 회의록 템플릿은 이미 있는데 placeholder 채우기와 구조 유지가 번거로울 때
- 요약 결과를 그대로 믿기보다, 어느 발화를 근거로 썼는지 나중에 검토할 수 있어야 할 때
- 여러 전사 파일이나 여러 템플릿 중 하나를 골라야 해서 자동 추정이 위험할 때

## 예시 요청

아래처럼 요청할 수 있습니다.

```text
인프라 스터디 킥오프 미팅 파일로 회의록 작성해줘.
```

```text
다운로드 폴더에 있는 클로바노트 전사 파일로 general.md 양식에 맞춰 회의록 만들어줘.
```

```text
회의록은 ./minutes 폴더 아래에 저장해줘.
```

경로가 모호하면 스킬은 후보를 ordered list로 보여 주고, 번호 또는 텍스트로 선택하도록 요청해야 합니다.

## 결과 예시

이 저장소에는 샘플 전사 파일, 템플릿, 생성 결과가 함께 들어 있습니다.

- 템플릿 예시: [tests/general.md](./tests/general.md)
- 전사 예시: [tests/인프라 스터디 킥오프 미팅.txt](./tests/%EC%9D%B8%ED%94%84%EB%9D%BC%20%EC%8A%A4%ED%84%B0%EB%94%94%20%ED%82%A5%EC%98%A4%ED%94%84%20%EB%AF%B8%ED%8C%85.txt)
- 생성 결과 예시: [tests/회의록_2026-04-13_인프라 스터디 킥오프 미팅.md](./tests/%ED%9A%8C%EC%9D%98%EB%A1%9D_2026-04-13_%EC%9D%B8%ED%94%84%EB%9D%BC%20%EC%8A%A4%ED%84%B0%EB%94%94%20%ED%82%A5%EC%98%A4%ED%94%84%20%EB%AF%B8%ED%8C%85.md)

## 지원 에이전트

현재 설치 가이드는 아래 에이전트를 대상으로 정리되어 있습니다.

- Codex
- Claude Code
- Antigravity
- OpenCode

## 저장소 구성

```text
.
├── README.md
├── INSTALL.md
├── SKILL.md
├── references/
└── tests/
```

## 참고 문서

- [SKILL.md](./SKILL.md)
- [INSTALL.md](./INSTALL.md)
- [references/clova-note-format.md](./references/clova-note-format.md)
- [references/verifiable-timestamps.md](./references/verifiable-timestamps.md)
- [references/request-examples.md](./references/request-examples.md)
