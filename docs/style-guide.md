# style-guide — 19_newItsm 대시보드

> **원칙**: `inputs/proto.html` '대시보드 (New)' 의 HTML·CSS·UI/UX 를 그대로 쓴다.
> CSS 는 proto 번들 템플릿의 `<style>` 5벌을 `outputs/index.html` 에 원문 그대로 옮겼고, 별도 토큰·스타일 파일은 두지 않는다.
> 예외는 CLAUDE.md 규칙인 구현 메뉴 강조 한 줄(`--c-menu-impl` #FFD400)뿐이다.

## 1. 색·크기
proto CSS 의 토큰을 그대로 쓴다 — `--color-*`(background·card·border·primary·success·warning·destructive·info),
`--chart-1~6`(#3f5d8a #6f9fb5 #7f9c6a #c3a05a #a3717f #77748f), `--menu-*`, `--d-*`(sidebar 240px · header 48px · section-gap 12px).

## 2. proto 마크업 대응표 (index.html 조각 함수)
| 함수 | proto 원본 | 비고 |
|---|---|---|
| `dashHead` | `[data-dash-head]` 현황판 머리 | 제목 + 역할 배지 + 설명 + (관리자만) 기간 단추 + 편집 |
| `wgt` | `[data-wgt-id]` 카드 | `rounded-xl border bg-card` → 머리(px-3 py-1.5, 기간 배지) → 본문(p-2) → 꼬리(`data-wgt-note`) |
| `tile` | WGT-053 머리줄 요약 타일 | `text-2xl font-bold` 숫자 + 단위 + 우측 2줄 보조, 경고는 `data-warn` 삼각형 |
| `xtb` | `.x-tb` 표 | 첫 열·`x-l` 왼쪽 정렬, 0 은 `x-zero`, 합계는 `x-foot`, 4행 이상이면 `x-fill` |
| `steps` | WGT-001 `.x-steps` | 단계 카드 + `x-chev` |
| `hbars` | WGT-011 `.x-hb` | 가로 막대 순위 |
| `alerts` | WGT-052 `.x-alert` | 상태 배지 + 내용 목록 |
| `donutTable` | `.x-donut-table` | 도넛(라벨 끔) + 견본색 비율표 |
| `chart` | `.x-chart` + `itgChart` | 제품 chart-option.js, 계열색은 `--chart-N`(proto paintSeries) |
| `askBox`·`quickReq` | 서비스포털 (New) `[data-ask]`·`[data-quick-req]` | 사용자용 포털 상단 |
| 메뉴 | proto `MENU_BASE`/`MENU_SUB`/`MENU_ACTIVE` | 대분류 +/− 펼침, 활성 leaf `aria-current` |

격자: `grid gap-3`, `grid-template-columns: repeat(12, minmax(0,1fr))`, `grid-auto-rows: 86px`, 카드는 `grid-area` 로 배치.

## 3. 사용자용 / 관리자용 구분 (proto 어휘 안에서)
- 현황판 머리 배지: 사용자용 = `bg-info/10 text-info` 「사용자용」, 관리자용 = `bg-primary/10 text-primary` 「관리자용」
- 기간 단추(일/주/월/분기): 관리자용에만 둔다 — 사용자용은 proto TPL-5 내 업무판처럼 기간 창이 없다
- 카드 머리 배지(`data-period-badge`): 본인 위젯 「본인」, 부서 위젯 「부서」·「부서원」, 월간 지표 「금월」·「최근 6개월」
- 헤더 사용자 칩: 사용자용 = 이서연 @seoyeon, 관리자용 = 박정훈 @jhpark (로그인 시점)
- 머리 우측 범위 표기: 「이서연 본인 기준」 / 「인프라운영팀 부서원 8명 기준」
