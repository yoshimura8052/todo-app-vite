Todo App（Auth × Supabase対応版）





Vue3（Composition API）とViteを用いて開発したSPA形式のタスク管理アプリです。

Supabaseを用いたユーザー認証およびデータベース連携を実装し、実務を想定したCRUD設計・アクセス制御（RLS）まで対応しています。







🔗 Demo

https://yoshimura8052.github.io/todo-app-vite/



💻 GitHub

https://github.com/yoshimura8052/todo-app-vite









🛠 Tech Stack





Vue 3（Composition API）
Vite
JavaScript（ES6）
Supabase（Auth / Database / RLS）
localStorage
Git / GitHub










✨ Features





ユーザー認証（新規登録 / ログイン / ログアウト）
ユーザーごとのタスク管理（RLSによるデータ分離）
タスク追加 / 削除 / 編集（CRUD対応）
完了・未完了の状態管理（DB連動）
フィルター機能（All / Active / Completed）
残タスク数のリアルタイム表示（computed使用）
完了タスクのみ削除（DB連動）
全削除機能（確認ダイアログ付き / DB連動）
ダークモード切替（状態永続化）
トランジションアニメーション










🧠 What I Focused On





Composition APIを用いた状態・ロジックの整理
App.vueへの状態集約とコンポーネント分割による責務分離設計
computedによる効率的な再レンダリング設計
async/awaitを用いた非同期API通信の実装
Supabase RLSによるユーザー単位のアクセス制御
DB更新後の即時UI反映（リアクティブ設計）
UI状態（ダークモード）を含めた永続化設計
実務を意識したCRUD構成とエラーハンドリング
