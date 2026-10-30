# Impeccable 한국어 안내 (ilhae-ai 포크)

[pbakaus/impeccable](https://github.com/pbakaus/impeccable)를 포크해 한국어 화면 디자인 규칙을 더한 버전입니다. 원본 문서는 [README.md](README.md)와 [impeccable.style/docs](https://impeccable.style/docs)에 있습니다.

Impeccable은 코딩 에이전트(Claude Code, Cursor, Codex CLI 등)에 디자인 어휘를 붙여 주는 스킬입니다. "좀 더 세련되게"처럼 막연하게 말하는 대신 `/impeccable bolder 가격 카드`처럼 명령과 대상을 지정하고, `critique`·`audit`으로 리뷰를 받고, 결정적 규칙 기반 감지기로 AI가 만든 티가 나는 패턴(AI slop)을 잡아냅니다.

## 이 포크에서 달라진 점

원본 파일은 고치지 않고 아래만 추가했습니다. upstream을 그대로 따라가기 위해서입니다.

| 파일 | 내용 |
|---|---|
| `skill/reference/korean.md` | 한국어 화면 규칙. 한글 조판(글줄 길이, 행간, `word-break: keep-all`, 자간, 이탤릭 금지), 국내 폰트 선택과 라이선스·웹폰트 로딩, 한국어 카피 슬롭(말투 혼용, 번역투, 직역 마케팅 문구, 장식용 영어 라벨), 조사 처리·IME 입력·날짜와 금액 형식 같은 한국어 하드닝 |
| `skill/SKILL.src.md` | Setup에 4번 항목 한 줄 추가. 화면 카피가 한국어면(`lang="ko"`, PRODUCT.md에 한국어 사용자 명시, 대상 텍스트 대부분이 한글) `korean.md`를 읽게 함 |
| `README.ko.md` | 이 문서 |

루트의 `.claude/`, `.cursor/`, `plugin/` 같은 폴더는 `skill/`에서 빌드되는 산출물이라, 위 변경을 반영해 다시 생성해 두었습니다.

감지기 엔진(Rust)은 손대지 않았습니다. upstream 엔진이 이미 한글을 CJK로 인식해 글줄 길이·양쪽 정렬·자간 관련 검사를 따로 처리합니다.

## 설치

> **주의:** `npx impeccable install`과 `npx impeccable update`는 upstream(pbakaus) 릴리스에서 서명된 번들을 내려받습니다. 이 포크의 한국어 규칙이 들어가지 않으니, 포크 버전을 쓰려면 아래 방법 중 하나로 설치하세요.

### Claude Code 플러그인 (권장)

```
/plugin marketplace add ilhae-ai/impeccable
/plugin install impeccable@impeccable
```

스킬, 서브에이전트, 디자인 훅이 함께 설치됩니다. 이미 `pbakaus/impeccable` 마켓플레이스를 추가해 두었다면 이름(`impeccable`)이 겹치니 먼저 `/plugin marketplace remove impeccable`로 지우고 추가하세요. 엔진 바이너리는 첫 실행 때 upstream 릴리스에서 한 번 내려받습니다.

### 팀 단위로 고정하기 (git submodule)

```bash
git submodule add https://github.com/ilhae-ai/impeccable vendor/impeccable
npx impeccable link --source=vendor/impeccable --providers=claude,cursor
```

`link`는 스킬만 연결하고 훅은 설치하지 않습니다.

### 수동 복사

이 레포를 클론해서 사용하는 도구의 폴더에서 `skills/impeccable`을 프로젝트로 복사합니다. 예를 들어 Claude Code라면:

```bash
mkdir -p your-project/.claude/skills
cp -r .claude/skills/impeccable your-project/.claude/skills/
```

도구별 폴더 위치는 [README.md의 Manual copy 표](README.md#installation)를 보세요. 수동 복사는 훅과 서브에이전트가 빠집니다.

## 시작하기

프로젝트마다 한 번 실행합니다.

```
/impeccable init
```

코드를 읽고 추론할 수 없는 것(누가 쓰는 제품인지, 무엇을 해야 하는지, 제약 조건)만 물어본 뒤 `PRODUCT.md`를 씁니다. 한국어 서비스라면 이때 사용자와 카피 언어가 한국어라고 답해 두세요. 이후 명령이 `korean.md`를 자동으로 읽는 근거가 됩니다. 기존 화면의 시각 체계는 `/impeccable document`로 `DESIGN.md`에 정리해 둡니다.

그다음부터는 명령과 대상을 지정합니다. 대상이 좁을수록 결과가 좋습니다.

```
/impeccable critique 온보딩 흐름
/impeccable quieter 랜딩 페이지
/impeccable polish 설정 화면
/impeccable harden 결제 화면
```

명령 없이 하고 싶은 걸 그냥 말해도 됩니다. `/impeccable`만 입력하면 명령 목록이 나옵니다.

## 명령어 한눈에 보기

| 분류 | 명령 | 하는 일 |
|---|---|---|
| 방향 잡기 | `bolder` | 무난하고 밋밋한 디자인을 과감하게 |
| | `quieter` | 요란한 디자인을 차분하게 |
| | `distill` | 필요 없는 요소를 덜어내 핵심만 남김 |
| | `colorize` | 무채색 화면에 의도 있는 색을 넣음 |
| | `typeset` | 폰트, 위계, 크기를 바로잡음 |
| | `layout` | 간격과 리듬, 시각적 위계를 정리 |
| | `animate` | 전환과 인터랙션 피드백을 추가 |
| | `delight` | 기억에 남는 개성을 더함 |
| | `overdrive` | 셰이더, 스프링 물리, 스크롤 연동 효과까지 밀어붙임 |
| 리뷰 | `critique` | 사용성 휴리스틱으로 점수를 매기고 고칠 순서를 정함 |
| | `audit` | 접근성·성능·테마·반응형을 기술적으로 점검 (P0~P3) |
| 마무리 | `polish` | 배포 전 마지막 다듬기 |
| | `harden` | 오류 처리, 다국어, 넘침, 예외 상황 대비 |
| | `clarify` | 모호한 UX 문구를 다시 씀 |
| | `adapt` | 화면 크기와 기기에 맞게 조정 |
| | `optimize` | 로딩과 렌더링 성능 개선 |
| | `onboard` | 첫 사용 흐름과 빈 상태 설계 |
| 라이브 반복 | `live` | 브라우저에서 요소를 골라 변형안을 바로 바꿔 끼워 봄 |
| | `generate` | 지정한 요소의 변형안을 여러 개 만들어 비교 |
| 기획·설정 | `shape` | 코드 전에 UX를 설계 |
| | `init` | `PRODUCT.md` 작성 |
| | `document` | 기존 코드에서 `DESIGN.md` 생성 |
| | `extract` | 반복되는 패턴을 디자인 시스템으로 추출 |

`craft`는 더 이상 쓰지 않는 별칭입니다. 자주 쓰는 명령은 `/impeccable pin audit`처럼 고정하면 `/audit`으로 바로 부를 수 있습니다. Codex에서는 `/impeccable` 대신 `$impeccable`을 씁니다.

## 감지기 단독 실행

에이전트 없이 CLI만으로도 돌릴 수 있습니다. LLM이나 API 키가 필요 없습니다.

```bash
npx impeccable detect src/                     # 디렉터리 스캔
npx impeccable detect http://localhost:5173    # 렌더링된 페이지 스캔 (대비, 작은 글씨 등 포함)
npx impeccable detect --json .                 # JSON 출력
npx impeccable detect --list-rules             # 전체 규칙 목록
```

종료 코드 `2`는 발견 사항 있음, `1`은 스캔 실패입니다. 감지기는 엔진 기능이라 포크와 upstream이 같습니다.

## upstream 동기화

이 포크는 원본 파일을 고치지 않는 것을 원칙으로 합니다. 동기화 순서는 다음과 같습니다.

```bash
git fetch upstream
git merge upstream/main
# 생성 산출물에서 충돌이 나면 upstream 쪽을 받고 다시 빌드
bun install && bun run build:skills:release
```

충돌이 날 수 있는 원본 파일은 `skill/SKILL.src.md`의 Setup 4번 줄 하나뿐입니다.

## 라이선스

원본과 같은 Apache 2.0입니다. [LICENSE](LICENSE)와 [NOTICE.md](NOTICE.md)를 보세요.
