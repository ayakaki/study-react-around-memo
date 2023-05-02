# research-react-around-memo

パフォーマンス改善に有効なメモ化関連（React memo, useCallback, useMemo）の動作を調査し、整理した。

## SUMMARY

下記の話は、簡略化のため、props は言及する値・関数のみを渡していることを前提とする。

### ①React memo

- 親コンポーネントがレンダリングされた場合においても、props が変更されない限り、子コンポーネントの再レンダリングが走らない

### ②useCallback

- 親コンポーネントから props で関数が渡された場合において、親コンポーネントの再レンダリングが走っても、子コンポーネントの再レンダリングが走らない
  - ※ 通常、props にて関数が渡された場合、子コンポーネントをメモ化していても、親コンポーネントに再レンダリングが走れば、子コンポーネントは再レンダリングが走る
- ※ useCallback は子コンポーネントがメモ化されていることが前提

### ③useMemo

- 処理結果をメモするため、再レンダリングによる不要な計算が走らない

## MOTION

### ①React memo

#### 適用なしの場合

親コンポーネントのみに存在する state が更新され、親コンポーネントに再レンダリングが走った際、子コンポーネントも再レンダリングが走っている。

#### 適用ありの場合

親コンポーネントのみに存在する state が更新され、親コンポーネントに再レンダリングが走った際、小コンポーネントには再レンダリングが走っていない。

### ②useCallback

#### 適用なしの場合

親コンポーネントのみに存在する state が更新され、親コンポーネントに再レンダリングが走った際、子コンポーネントも再レンダリングが走っている。

#### 適用ありの場合

親コンポーネントのみに存在する state が更新され、親コンポーネントに再レンダリングが走った際、小コンポーネントには再レンダリングが走っていない。

### ③useMemo

#### 適用なしの場合

コンポーネントの state に変更があり、コンポーネントに再レンダリングが走った際、都度処理が実行されている。

#### 適用ありの場合

コンポーネントの state に変更があり、コンポーネントに再レンダリングが走った際、処理が実行されていない。

## URL

| 分類        | 項目     | URL                                                                  |
| ----------- | -------- | -------------------------------------------------------------------- |
| React.memo  | 適用なし | [/react-memo/not-apply](http://localhost:3000/react-memo/not-apply)  |
|             | 適用あり | [/react-memo/apply](http://localhost:3000/react-memo/apply)          |
| useCallback | 適用なし | [/usecallback/not-apply](http://localhost:3000/react-memo/not-apply) |
|             | 適用あり | [/usecallback/apply](http://localhost:3000/react-memo/apply)         |
| useMemo     | 適用なし | [/usememo/not-apply](http://localhost:3000/usememo/not-apply)        |
|             | 適用あり | [/usememo/apply](http://localhost:3000/usememo/apply)                |
