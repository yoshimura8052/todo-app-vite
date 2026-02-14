# Todo App

Vue3（Composition API）とViteを用いて開発したSPA形式のタスク管理アプリです。 
状態管理・フィルタリング・データ永続化を意識し、実務を想定した設計で実装しました。

---

## 🔗 Demo
https://yoshimura8052.github.io/todo-app-vite/

## 💻 GitHub
https://github.com/yoshimura8052/todo-app-vite

---

## 🛠 Tech Stack
- Vue 3（Composition API）
- Vite
- JavaScript（ES6）
- localStorage
- Git / GitHub

---

## ✨ Features
- タスク追加 / 削除
- 完了・未完了の状態管理
- フィルター機能（All / Active / Completed）
- 残タスク数のリアルタイム表示（computed使用）
- 完了タスクのみ削除
- 全削除機能（確認ダイアログ付き）
- ダークモード切替（状態永続化）
- トランジションアニメーション
- localStorageによるデータ永続化

---

## 🧠 What I Focused On
- Composition APIを用いた状態・ロジックの整理
- computedによる効率的な再レンダリング設計
- watch（deep）を活用した正確な状態監視
- UI状態（ダークモード）も含めた永続化設計
- 未完了タスクを上位表示するソート処理実装
- UXを意識したシンプルなUI設計
