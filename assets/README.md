# SUDOKU Journey — 에셋 가이드

모든 파일은 **WebP** 포맷입니다. 투명 배경 지원, PNG 대비 용량 80% 절감.
(Chrome / Safari 14+ / Firefox / Edge 전부 지원)

## 폴더 구조

```
assets/
├── bg/       배경 (데스크톱/모바일 분기)
├── stones/   스테이지 돌 + 효과
├── ui/       타이틀 로고, 나무 안내판
└── ref/      ⚠️ 구현용 아님 — 디자인 참고용
```

## 파일 목록

### bg/ — 배경
| 파일 | 크기 | 용도 |
|---|---|---|
| `bg-desktop.webp` | 1487×1058 | 가로 화면 (768px 이상) |
| `bg-mobile.webp` | 1080×1920 | 세로 화면 (767px 이하) |

### stones/ — 스테이지 돌
| 파일 | 크기 | 용도 |
|---|---|---|
| `stone-1` ~ `stone-5.webp` | 256×256 | 단계 번호 돌 |
| `stone-base.webp` | 256×256 | 숫자 없는 기본 돌 |
| `fx-selected.webp` | 256×256 | 노랑 링 (현재 스테이지) |
| `fx-locked.webp` | 256×256 | 파랑 링 (잠금) |
| `stone-selected.webp` | 256×256 | 돌+노랑링 합본 |
| `stone-locked.webp` | 256×256 | 돌+파랑링 합본 |
| `icon-lock.webp` | 96×96 | 자물쇠 (큰 사이즈) |
| `icon-lock-sm.webp` | 64×64 | 자물쇠 배지 |

합본(`stone-selected` / `stone-locked`)은 정적 표시용입니다.
효과에 애니메이션을 줄 거면 **분리본을 겹쳐 쓰세요.**

### ui/
| 파일 | 크기 | 비고 |
|---|---|---|
| `title-logo.webp` | 1024×438 | 원본 1831×784에서 축소 — 품질 충분 |
| `sign-board.webp` | 336×288 | ⚠️ 원본 168×144를 2배 확대 — 재생성 권장 |

### ref/ — 구현하지 마세요
`difficulty-panel` / `btn-reset`은 **이미지로 쓰면 안 되는 UI**입니다.
`0/150` 숫자가 진행에 따라 바뀌고, 선택·hover 상태가 필요합니다.
아래 색상값으로 CSS 구현하시고, 이 파일은 디자인 확인용으로만 보세요.

## 상태별 조합

| 상태 | 구성 |
|---|---|
| 클리어 | `stone-N` |
| 현재 | `fx-selected` + `stone-N` |
| 잠금 | `fx-locked` + `stone-N` + `icon-lock-sm` |

z-index: 효과(0) → 돌(1) → 배지(2)

## 스테이지 좌표 (% 기준)

배경마다 강의 경로가 달라 좌표가 다릅니다.

```js
const STAGES = {
  desktop: [ {x:73,y:9}, {x:64,y:29}, {x:53,y:48}, {x:37,y:66}, {x:22,y:87} ],
  mobile:  [ {x:59,y:14}, {x:52,y:32}, {x:42,y:51}, {x:46,y:70}, {x:37,y:88} ]
};
```

## 색상 토큰

```css
:root {
  --panel-bg:  #F8EFD8;
  --easy:      #5A9C34;
  --easy-dark: #2C7819;
  --normal:    #FCEFCD;
  --hard:      #FAC5BD;
  --btn-green: #4B9430;
  --overlay:   rgba(18, 30, 45, .28); /* 배경 위 딤 — 돌 가독성용 */
}
```

## 주의사항

- 경로는 **상대경로**로 (`assets/stones/stone-1.webp`). 앞에 `/` 금지.
- 파일명 **대소문자 구분** — GitHub Pages는 로컬과 다르게 엄격합니다.
- 배경 위에 `--overlay` 딤을 깔아야 돌이 배경 바위와 구분됩니다.
