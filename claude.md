# JOOUI React 프로젝트 규칙

## 프로젝트 개요
jooui(vanilla JS) UI 컴포넌트를 React + TypeScript + WAI-ARIA로 변환하는 라이브러리.

## 기술 스택
- React 18 + TypeScript (함수형 컴포넌트 + hooks)
- Vite 5
- SCSS Modules (`.module.scss`)
- Storybook 8

## 컴포넌트 파일 구조
새 컴포넌트는 항상 이 구조로 생성한다:

```
src/components/ComponentName/
├── ComponentName.tsx          # 컴포넌트 본체
├── ComponentName.module.scss  # 스타일 (SCSS)
├── ComponentName.stories.tsx  # Storybook story
└── index.ts                   # named export
```

컴포넌트 추가 후 `src/components/index.ts`에 export를 반드시 추가한다.

## SCSS 규칙
- 공통 변수는 `src/styles/_variables.scss`를 `@use`로 불러온다
- 컴포넌트별 로컬 변수는 선언하지 않는다 (변수 파일 사용)
- 네스팅으로 상태/variants 표현 (`&:hover`, `&.primary`)

```scss
@use '../../styles/variables' as v;

.component {
  color: v.$color-primary;
}
```

## TypeScript 규칙
- props는 `interface ComponentNameProps`로 선언
- `any` 타입 금지 — `unknown` 또는 구체적인 타입 사용
- HTML 요소를 확장할 때는 `extends React.HTMLAttributes<HTMLElement>` 사용
- `...rest` spread로 HTML 속성 전달 허용

## WAI-ARIA 필수 포함
- 적절한 `role` 부여
- 상태 속성: `aria-selected`, `aria-expanded`, `aria-disabled` 등
- 키보드 인터랙션: Tab / Arrow keys / Enter / Space / Escape
- `focus-visible` 스타일 반드시 포함

## Storybook 규칙
- `title`은 `'JOOUI/ComponentName'` 형식
- `tags: ['autodocs']` 반드시 포함
- 기본 variants / 상태(disabled 등) / 조합 story 포함
- `argTypes`에 `onClick` 등 이벤트는 `{ action: 'eventName' }` 처리

## 금지 사항
- 클래스 컴포넌트 사용 금지
- `any` 타입 금지
- 불필요한 `useMemo` / `useCallback` 추가 금지
- `useEffect`에서 이벤트 리스너 등록 시 cleanup 필수
