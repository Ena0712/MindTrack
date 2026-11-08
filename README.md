# Piece in rest

**원본 프로젝트**
https://github.com/hbohare2004/MindTrack/tree/main

**vercel**
https://mind-track-five.vercel.app

**프로젝트 선정이유**
여러 프로젝트를 보던 중 디자인에 더 집중하고 싶어 다이어리와 뽀모도로 스타일의 프로젝트들을 위주로 찾아봤고, 기본 레이아웃과 디자인 색상이 가장 맘에 들고 원하던 디자인으로 변경이 용이할 것 같아 이 프로젝트를 선택하였다.

**설치**
별도의 방법이 필요없이 fork함.

**프로젝트 구조**

| `src/components/MoodSelector.jsx` | 기분 버튼 6개를 화면에 그리고, 버튼을 누르면 부모에게 눌린 기분을 전달 |
| `src/index.css` | 앱 전체에 적용되는 css 스타일. `:root`에 색상, 투명도, 모서리 둥글기 같은 CSS 변수, `body`의 그라데이션 배경과 `#root`의 레이아웃, 스크롤바 모양을 설정한다. |
| `src/App.css` | 컴포넌트별 css. 헤더, 기분 선택, 기분 기록, 타이머, 통계 카드 등 섹션별로 나뉘어 있고, 색은 `index.css`에서 가져옴. 화면 크기에 따른 반응형 규칙(768px, 480px, 360px) |


**컴포넌트**

### `Header`

- 헤더 컴포넌트.
- 아이콘, 제목, 설명을 출력.
- `glass-card header` 클래스를 사용.

### `MoodSelector`

- 기분 버튼을 누르는 컴포넌트.
- `onAddMood`를 props로 받음. 기분을 저장하는 일은 부모가 맡고, 이 컴포넌트는 "어떤 기분인지"만 확인.
- `moods` 배열(Happy, Excited, Calm, Neutral, Sad, Stressed)을 기준으로 버튼이 있음.
- 각 버튼은 이모지와 이름을 보여 주고, 클릭하면 `onAddMood(label, emoji)`를 호출함.


**코드 분석**

```jsx
<div className="mood-selector__grid">
  {moods.map((mood) => (
    <button
      key={mood.label}
      className="mood-btn"
      onClick={() => onAddMood(mood.label, mood.emoji)}
    >
      <span className="mood-btn__emoji">{mood.emoji}</span>
      <span className="mood-btn__label">{mood.label}</span>
    </button>
  ))}
</div>
```

### 동작 원리

**배열로 버튼 만들기**: `moods`는 `{ label, emoji }` 객체 6개가 든 배열. `map`이 배열의 각 항목을 `<button>` 으로 바꿈. 그래서 버튼 6개를 직접 쓰지 않아도 됩니다.

새로운 기분을 추가하려면 `moods` 배열에 `{ label: "...", emoji: "..." }` 추가하면 됨.

<hr>/
**변경**


| `src/index.css` | `:root` CSS 변수 21개 (색상, 투명도, 모서리 둥글기) |
| `src/App.css` | 컴포넌트 스타일 4개 속성 (헤더 아이콘, 타이머 버튼) |
| `src/components/Header.jsx` | 아이콘 이모지, 제목, 부제목 텍스트 |


**색상**

| `--primary` | `#6c5ce7` | `#b170ca` |
| `--primary-light` | `#a29bfe` | `#cdb6ea` |
| `--primary-dark` | `#4834d4` | `#44284d` |
| `--accent` | `#fd79a8` | `#da95ad` |
| `--accent-light` | `#fab1a0` | `#d3aca3` |
| `--success` | `#00b894` | `#8ec4b9` |
| `--warning` | `#fdcb6e` | `#e7cb98` |
| `--danger` | `#e17055` | `#e59480` |
| `--bg-gradient-start` | `#0f0c29` | `#bc93cd` |
| `--bg-gradient-mid` | `#302b63` | `#d5a4c8` |
| `--bg-gradient-end` | `#24243e` | `#e79cbb` |

**투명도**

| `--glass-bg` | `rgba(255, 255, 255, 0.06)` | `rgba(255, 255, 255, 0.103)` |
| `--glass-border` | `rgba(255, 255, 255, 0.1)` | `rgba(255, 255, 255, 0.162)` |
| `--text-secondary` | `rgba(255, 255, 255, 0.7)` | `rgba(255, 255, 255, 0.809)` |
| `--text-muted` | `rgba(255, 255, 255, 0.4)` | `rgba(255, 255, 255, 0.616)` |

**radius**

| `--radius-sm` | `12px` | `10px` |
| `--radius-md` | `16px` | `14px` |
| `--radius-lg` | `24px` | `22px` |
| `--radius-xl` | `32px` | `30px` |


| `.header__icon` | `font-size` | `3rem` | `6rem` |
| `.header__icon` | `margin-bottom` | `0.5rem` | `0.3rem` |
| `.header__icon` | `animation` | `pulse 3s ease-in-out infinite` | `pulse 2s ease-in-out infinite` |
| `.focus-timer__btn` | `background` | `rgba(255, 255, 255, 0.04)` | `rgba(255, 255, 255, 0.163)` |

```diff
 .header__icon {
-  font-size: 3rem;
+  font-size: 6rem;
   display: block;
-  margin-bottom: 0.5rem;
-  animation: pulse 3s ease-in-out infinite;
+  margin-bottom: 0.3rem;
+  animation: pulse 2s ease-in-out infinite;
 }

 .focus-timer__btn {
-  background: rgba(255, 255, 255, 0.04);
+  background: rgba(255, 255, 255, 0.163);
 }
```

| `.header__icon` | 🧠 | 🪷 |
| `.header__title` | `MindTrack` | `Piece in rest` |
| `.header__subtitle` | `Track your mood & productivity` | `Find little pieces of peace in you with rest` |

```diff
 function Header() {
   return (
     <header className="glass-card header">
-      <span className="header__icon">🧠</span>
-      <h1 className="header__title">MindTrack</h1>
-      <p className="header__subtitle">Track your mood & productivity</p>
+      <span className="header__icon">🪷</span>
+      <h1 className="header__title">Piece in rest</h1>
+      <p className="header__subtitle">Find little pieces of peace in you with rest</p>
     </header>
   );
 }
```
**리뷰**
오픈소스 프로젝트를 수정하면서 큰 어려움 없이 수정할 수 있었고, 오히려 프로젝트를 분석하고 코드를 뜯어 보며 읽는 것이 재미있었다. timer의 활용법과 버튼의 활용법, 여러 디자인 적인 부분을 배울 수 있었고, 불투명도와 같은 색상활용과 같은 것도 새로 접할 수 있었다.