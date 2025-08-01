---
theme: default
background: '#1a1a2e'
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Vue Router 入門
  Vue.js の公式ルーティングライブラリを初心者向けに解説
drawings:
  persist: false
transition: slide-left
title: Vue Router 入門
colorSchema: dark
fonts:
  sans: 'Noto Sans JP'
  mono: 'Fira Code'
---

# Vue Router 入門

<div class="text-4xl text-blue-400 font-bold mt-8">
  シングルページアプリケーションの<br/>ナビゲーションを簡単に
</div>

<div class="mt-16">
  <span class="text-gray-400">Vue.js 公式ルーティングライブラリ</span>
</div>

<style>
.slidev-layout {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
}
</style>

---
layout: two-cols
---

# SPAとは？

<div class="text-xl text-gray-300 leading-relaxed">
単一のHTMLで複数画面を実現する<br/>モダンなWebアプリケーション
</div>

::right::

<div class="ml-8 mt-8">
  <div class="bg-blue-900/30 p-6 rounded-lg mb-4">
    <h3 class="text-blue-400 font-bold mb-2">従来のWeb</h3>
    <p class="text-sm">ページ遷移ごとに全体を再読み込み</p>
  </div>
  <div class="bg-green-900/30 p-6 rounded-lg">
    <h3 class="text-green-400 font-bold mb-2">SPA</h3>
    <p class="text-sm">必要な部分だけを動的に更新</p>
  </div>
</div>

<style>
.slidev-layout {
  background: #0f0f23;
}
h1 {
  background: linear-gradient(45deg, #60a5fa, #34d399);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 3rem;
}
</style>

---

# なぜルーティングが必要？

<div class="grid grid-cols-3 gap-6 mt-12">
  <div class="bg-gradient-to-br from-blue-600/20 to-blue-800/20 p-8 rounded-xl">
    <div class="text-4xl mb-4">🔗</div>
    <h3 class="text-xl font-bold mb-2">URL管理</h3>
    <p class="text-sm opacity-80">各画面に固有のURLを割り当て、ブックマーク可能に</p>
  </div>
  <div class="bg-gradient-to-br from-green-600/20 to-green-800/20 p-8 rounded-xl">
    <div class="text-4xl mb-4">📱</div>
    <h3 class="text-xl font-bold mb-2">履歴管理</h3>
    <p class="text-sm opacity-80">ブラウザの戻る・進むボタンが期待通りに動作</p>
  </div>
  <div class="bg-gradient-to-br from-purple-600/20 to-purple-800/20 p-8 rounded-xl">
    <div class="text-4xl mb-4">🛡️</div>
    <h3 class="text-xl font-bold mb-2">アクセス制御</h3>
    <p class="text-sm opacity-80">認証が必要なページへの自動リダイレクト</p>
  </div>
</div>

<style>
.slidev-layout {
  background: #0f0f23;
}
h1 {
  color: #e0e0e0;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}
</style>

---

# セットアップ

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <h3 class="text-2xl font-bold text-blue-400 mb-4">1. インストール</h3>
    <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto"><code class="language-bash">npm install vue-router@4</code></pre>
  </div>
  <div>
    <h3 class="text-2xl font-bold text-green-400 mb-4">2. プロジェクトへの追加</h3>
    <pre class="bg-gray-900 p-4 rounded-lg overflow-x-auto"><code class="language-bash"># Vue CLIの場合
vue add router</code></pre>
  </div>
</div>

<div class="mt-12 p-6 bg-yellow-900/20 rounded-lg border border-yellow-600/40">
  <p class="text-yellow-400 font-bold">💡 ポイント</p>
  <p class="text-sm mt-2">Vue 3 には Vue Router 4 を使用します</p>
</div>

<style>
.slidev-layout {
  background: #0f0f23;
}
h1 {
  color: #e0e0e0;
  font-size: 2.5rem;
}
</style>

---

# 基本的なルート定義

<div class="mt-6">
  <p class="text-xl text-gray-300 mb-6">ルーターの設定方法を理解しよう</p>

```js
// router/index.js
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'Home',
    component: () => import('@/views/Home.vue')
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('@/views/About.vue')
  }
]
```

<div class="mt-6 p-4 bg-yellow-900/20 rounded-lg border border-yellow-600/40">
  <p class="text-yellow-400 font-bold">💡 遅延読み込みで初期ロードを最適化</p>
</div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# ルーターの作成とエクスポート

<div class="mt-8">
  <h3 class="text-2xl text-green-400 mb-6">ルーターインスタンスの生成</h3>

```js
// router/index.js (続き)
const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```

<div class="grid grid-cols-2 gap-8 mt-12">
  <div class="bg-blue-900/20 p-6 rounded-lg">
    <h4 class="text-blue-400 font-bold mb-3">createWebHistory()</h4>
    <p class="text-sm">HTML5 History APIを使用した標準的な履歴管理</p>
  </div>
  <div class="bg-green-900/20 p-6 rounded-lg">
    <h4 class="text-green-400 font-bold mb-3">routes配列</h4>
    <p class="text-sm">パスとコンポーネントの対応関係を定義</p>
  </div>
</div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# アプリへの組み込み

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <h3 class="text-xl text-blue-400 mb-4">main.js</h3>

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

createApp(App)
  .use(router)
  .mount('#app')
```

  </div>
  <div>
    <h3 class="text-xl text-green-400 mb-4">App.vue</h3>

```vue
<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>
```

  </div>
</div>

<div class="mt-8 flex gap-6">
  <div class="flex-1 bg-blue-900/30 p-4 rounded-lg">
    <code class="text-blue-400">&lt;router-link&gt;</code>
    <p class="text-sm mt-2">ナビゲーション用のリンク</p>
  </div>
  <div class="flex-1 bg-green-900/30 p-4 rounded-lg">
    <code class="text-green-400">&lt;router-view&gt;</code>
    <p class="text-sm mt-2">現在のルートを表示</p>
  </div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# 動的ルーティング

<div class="mt-8">
  <h3 class="text-2xl text-blue-400 mb-6">URLパラメータを使った動的ページ</h3>

```js
const routes = [
  {
    path: '/user/:id',
    component: UserProfile
  }
]
```

<div class="grid grid-cols-3 gap-4 my-8">
  <div class="bg-blue-900/30 p-4 rounded text-center">
    <div class="text-sm opacity-60">URL</div>
    <div class="font-mono">/user/123</div>
  </div>
  <div class="text-2xl self-center text-center">→</div>
  <div class="bg-green-900/30 p-4 rounded text-center">
    <div class="text-sm opacity-60">パラメータ</div>
    <div class="font-mono">id: "123"</div>
  </div>
</div>

```vue
<template>
  <h1>ユーザー ID: {{ $route.params.id }}</h1>
</template>
```

</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# プログラムナビゲーション

<div class="mt-6">
  <p class="text-xl text-gray-300 mb-6">JavaScriptでページ遷移を制御</p>

```js
// 文字列パス
router.push('/users/123')

// オブジェクト形式
router.push({ 
  name: 'User',
  params: { id: 123 }
})

// クエリ付き
router.push({
  path: '/search',
  query: { q: 'vue' }
})
// → /search?q=vue
```
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# ナビゲーションメソッド

<div class="mt-8">
  <p class="text-xl text-gray-300 mb-8">利用可能なルーティングメソッド</p>

  <div class="grid grid-cols-3 gap-6">
    <div class="bg-gray-800 p-6 rounded-lg text-center">
      <code class="text-blue-400 text-lg">push()</code>
      <p class="text-sm mt-3">新しい履歴を追加</p>
      <p class="text-xs text-gray-400 mt-2">「戻る」で前のページに</p>
    </div>
    <div class="bg-gray-800 p-6 rounded-lg text-center">
      <code class="text-green-400 text-lg">replace()</code>
      <p class="text-sm mt-3">現在の履歴を置換</p>
      <p class="text-xs text-gray-400 mt-2">履歴に残らない</p>
    </div>
    <div class="bg-gray-800 p-6 rounded-lg text-center">
      <code class="text-purple-400 text-lg">back()</code>
      <p class="text-sm mt-3">前のページに戻る</p>
      <p class="text-xs text-gray-400 mt-2">ブラウザの戻るボタンと同じ</p>
    </div>
  </div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# ナビゲーションガード

<div class="mt-6">
  <p class="text-xl text-gray-300 mb-8">ルート遷移を制御して、アクセス管理を実現</p>
  
  <div class="grid grid-cols-2 gap-6">
    <div class="bg-blue-900/20 p-6 rounded-lg">
      <h3 class="text-blue-400 font-bold mb-4">グローバルガード</h3>

```js
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth && !isLoggedIn) {
    next('/login')
  } else {
    next()
  }
})
```

</div>
    <div class="bg-green-900/20 p-6 rounded-lg">
      <h3 class="text-green-400 font-bold mb-4">ルート単位ガード</h3>

```js
{
  path: '/admin',
  component: Admin,
  beforeEnter: (to, from, next) => {
    // 管理者チェック
    checkAdmin() ? next() : next('/403')
  }
}
```

</div>
  </div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# メタフィールドの活用

<div class="mt-8">

```js
const routes = [
  {
    path: '/dashboard',
    component: Dashboard,
    meta: { 
      requiresAuth: true,
      title: 'ダッシュボード'
    }
  }
]
```

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <h3 class="text-xl text-blue-400 mb-4">使用例: 認証チェック</h3>

```js
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth) {
    // 認証確認
  }
})
```

</div>
  <div>
    <h3 class="text-xl text-green-400 mb-4">使用例: タイトル設定</h3>

```js
router.afterEach((to) => {
  document.title = to.meta.title || 'My App'
})
```

</div>
</div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# ネストされたルート

<div class="mt-6">
  <p class="text-xl text-gray-300 mb-6">親子関係のあるルートを定義</p>

```js
const routes = [
  {
    path: '/user/:id',
    component: User,
    children: [
      {
        path: 'profile',
        component: UserProfile
      },
      {
        path: 'posts',
        component: UserPosts
      }
    ]
  }
]
```

<div class="mt-8 space-y-3">
  <div class="bg-gray-800 p-4 rounded">
    <code class="text-blue-400">/user/123</code>
    <span class="text-gray-400 ml-4">→ User コンポーネント</span>
  </div>
  <div class="bg-gray-800 p-4 rounded ml-6">
    <code class="text-green-400">/user/123/profile</code>
    <span class="text-gray-400 ml-4">→ UserProfile コンポーネント</span>
  </div>
  <div class="bg-gray-800 p-4 rounded ml-6">
    <code class="text-purple-400">/user/123/posts</code>
    <span class="text-gray-400 ml-4">→ UserPosts コンポーネント</span>
  </div>
</div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# トランジション効果

<div class="mt-8">

```vue
<router-view v-slot="{ Component }">
  <transition name="fade" mode="out-in">
    <component :is="Component" />
  </transition>
</router-view>
```

<div class="grid grid-cols-3 gap-4 mt-8">
  <div class="bg-blue-900/30 p-6 rounded text-center">
    <div class="text-2xl mb-2">📤</div>
    <p class="text-sm">現在のページが<br/>フェードアウト</p>
  </div>
  <div class="bg-gray-800/30 p-6 rounded text-center">
    <div class="text-2xl mb-2">⏱️</div>
    <p class="text-sm">トランジション<br/>実行中</p>
  </div>
  <div class="bg-green-900/30 p-6 rounded text-center">
    <div class="text-2xl mb-2">📥</div>
    <p class="text-sm">次のページが<br/>フェードイン</p>
  </div>
</div>

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
```

</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---

# 実践例: 認証システム

<div class="grid grid-cols-2 gap-6 mt-6">
  <div>
    <h3 class="text-lg text-blue-400 mb-3">ルート構成</h3>

```js
const routes = [
  { path: '/', component: Home },
  { path: '/login', component: Login },
  { 
    path: '/dashboard',
    component: Dashboard,
    meta: { requiresAuth: true }
  },
  {
    path: '/admin',
    component: Admin,
    meta: { 
      requiresAuth: true,
      requiresAdmin: true 
    }
  }
]
```

</div>
  <div>
    <h3 class="text-lg text-green-400 mb-3">認証フロー</h3>
    <div class="bg-gray-800/50 p-4 rounded">
      <div class="space-y-2 text-sm">
        <div class="flex items-center">
          <span class="text-blue-400">1.</span>
          <span class="ml-2">ユーザーがページにアクセス</span>
        </div>
        <div class="flex items-center">
          <span class="text-blue-400">2.</span>
          <span class="ml-2">認証状態をチェック</span>
        </div>
        <div class="flex items-center">
          <span class="text-blue-400">3.</span>
          <span class="ml-2">未認証なら /login へ</span>
        </div>
        <div class="flex items-center">
          <span class="text-blue-400">4.</span>
          <span class="ml-2">認証済みならアクセス許可</span>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
.slidev-layout { background: #0f0f23; }
h1 { color: #e0e0e0; }
</style>

---
layout: center
---

# まとめ

<div class="mt-8 max-w-3xl mx-auto">
  <div class="grid grid-cols-2 gap-8">
    <div class="bg-blue-900/20 p-8 rounded-xl">
      <h3 class="text-2xl text-blue-400 font-bold mb-4">基本機能</h3>
      <ul class="space-y-2 text-gray-300">
        <li>✅ ルート定義とコンポーネント紐付け</li>
        <li>✅ 動的ルーティング</li>
        <li>✅ プログラムナビゲーション</li>
      </ul>
    </div>
    <div class="bg-green-900/20 p-8 rounded-xl">
      <h3 class="text-2xl text-green-400 font-bold mb-4">応用機能</h3>
      <ul class="space-y-2 text-gray-300">
        <li>✅ ナビゲーションガード</li>
        <li>✅ ネストされたルート</li>
        <li>✅ トランジション効果</li>
      </ul>
    </div>
  </div>
  
  <div class="mt-12 text-center">
    <p class="text-xl text-gray-400">これでSPAの基本的なルーティングが実装できます！</p>
  </div>
</div>

<style>
.slidev-layout {
  background: linear-gradient(135deg, #0f0f23 0%, #1a1a2e 100%);
}
</style>

---
layout: center
---

# 次のステップ

<div class="mt-6 space-y-4 max-w-2xl mx-auto">
  <div class="bg-gradient-to-r from-blue-600/20 to-blue-800/20 p-4 rounded-xl">
    <h3 class="text-lg font-bold mb-1">📚 公式ドキュメント</h3>
    <p class="text-sm">https://router.vuejs.org/</p>
  </div>
  
  <div class="bg-gradient-to-r from-green-600/20 to-green-800/20 p-4 rounded-xl">
    <h3 class="text-lg font-bold mb-1">🛠️ 実践プロジェクト</h3>
    <p class="text-sm">ブログやタスク管理アプリを作ってみよう</p>
  </div>
  
  <div class="bg-gradient-to-r from-purple-600/20 to-purple-800/20 p-4 rounded-xl">
    <h3 class="text-lg font-bold mb-1">🚀 高度な機能</h3>
    <p class="text-sm">遅延読み込み、スクロール制御、ルートプリフェッチ</p>
  </div>
</div>

<div class="mt-8 text-center">
  <div class="text-2xl font-bold bg-gradient-to-r from-blue-400 to-green-400 bg-clip-text text-transparent">
    Happy Routing! 🚀
  </div>
</div>

<style>
.slidev-layout {
  background: linear-gradient(135deg, #0f0f23 0%, #1a1a2e 100%);
}
</style>
