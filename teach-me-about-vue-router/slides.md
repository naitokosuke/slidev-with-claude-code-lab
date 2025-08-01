---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Vue Router 入門
  Vue.js の公式ルーティングライブラリ Vue Router を学ぶための入門スライド
drawings:
  persist: false
transition: fade-out
title: Vue Router 入門
mdc: true
---

# Vue Router 入門

シングルページアプリケーションのルーティングを簡単に

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    はじめる <carbon:arrow-right class="inline"/>
  </span>
</div>

---
transition: fade-out
layout: default
---

# ルーティングとは？

<div class="grid grid-cols-2 gap-8">
<div>

## 従来のウェブページ

- ページごとに別々のHTMLファイル
- ページ遷移のたびにサーバーにリクエスト
- ページ全体が再読み込みされる

```html
<!-- index.html -->
<a href="about.html">About</a>

<!-- about.html -->
<a href="index.html">Home</a>
```

</div>
<div>

## SPAでのルーティング

- 1つのHTMLファイルで複数の画面を表現
- JavaScript でページ遷移を制御
- スムーズなユーザー体験

```js
// Vue Router を使った例
<router-link to="/about">About</router-link>
<router-link to="/">Home</router-link>
```

</div>
</div>

---
transition: fade-out
---

# なぜ Vue Router が必要？

<div class="space-y-6">

<v-clicks>

## 🚀 シングルページアプリケーション（SPA）の実現

ページ遷移時の再読み込みなしで、スムーズなユーザー体験を提供

## 🔗 URLとコンポーネントの紐付け

URLの変更に応じて適切なコンポーネントを表示

## 📱 ブラウザの履歴管理

「戻る」「進む」ボタンが期待通りに動作

## 🛡️ ナビゲーションガード

認証が必要なページへのアクセス制御など

</v-clicks>

</div>

---
transition: fade-out
---

# Vue Router のセットアップ

<div class="space-y-4">

## 1. インストール

```bash
npm install vue-router@4
```

## 2. ルーターの作成

```js {all|2-3|5-15|17-20|all}
// router/index.js
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('../views/About.vue') // 遅延読み込み
  }
]

const router = createRouter({
  history: createWebHistory(),
  routes
})
```

</div>

---
transition: fade-out
---

# アプリケーションへの組み込み

<div class="grid grid-cols-2 gap-4">

<div>

## main.js での設定

```js {all|1|5|all}
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

createApp(App)
  .use(router)
  .mount('#app')
```

</div>

<div>

## App.vue でのビュー表示

```vue {all|3|6|all}
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

<div class="mt-8 text-sm text-gray-600">

💡 `<router-link>` はナビゲーション用のリンクコンポーネント  
💡 `<router-view>` は現在のルートに対応するコンポーネントを表示

</div>

---
transition: fade-out
---

# 動的ルーティング

URLパラメータを使って動的なページを作成

<div class="grid grid-cols-2 gap-4 mt-8">

<div>

## ルート定義

```js
const routes = [
  {
    path: '/user/:id',
    name: 'User',
    component: User
  },
  {
    path: '/post/:id/comment/:commentId',
    name: 'PostComment',
    component: PostComment
  }
]
```

</div>

<div>

## コンポーネントでの使用

```vue
<template>
  <div>
    <h1>User ID: {{ $route.params.id }}</h1>
  </div>
</template>

<script>
export default {
  mounted() {
    console.log(this.$route.params.id)
  }
}
</script>
```

</div>

</div>

---
transition: fade-out
---

# プログラムによるナビゲーション

`router.push()` を使ってJavaScriptでページ遷移

```js {all|2-3|5-6|8-12|all}
// 文字列パス
router.push('/users/123')

// オブジェクト形式
router.push({ path: '/users/123' })

// 名前付きルート
router.push({ 
  name: 'User', 
  params: { id: 123 } 
})

// クエリパラメータ付き
router.push({ 
  path: '/search', 
  query: { q: 'vue' } 
})
// 結果: /search?q=vue
```

<div class="mt-8 flex gap-4">

<div class="flex-1">

### その他のメソッド

- `router.replace()` - 履歴を残さない
- `router.go(n)` - 履歴を n 個進む/戻る
- `router.back()` - 1つ前に戻る

</div>

</div>

---
transition: fade-out
---

# ナビゲーションガード

ルート遷移の前後に処理を実行

<div class="space-y-6">

## グローバルガード

```js
router.beforeEach((to, from, next) => {
  // 認証チェック
  if (to.meta.requiresAuth && !isAuthenticated()) {
    next('/login')
  } else {
    next()
  }
})
```

## ルート単位のガード

```js
{
  path: '/admin',
  component: Admin,
  beforeEnter: (to, from, next) => {
    // 管理者権限チェック
    if (hasAdminRole()) {
      next()
    } else {
      next('/403')
    }
  }
}
```

</div>

---
transition: fade-out
---

# ルートメタフィールド

ルートに追加情報を付与

```js {all|5-7|all}
const routes = [
  {
    path: '/admin',
    component: Admin,
    meta: { 
      requiresAuth: true,
      roles: ['admin']
    }
  },
  {
    path: '/profile',
    component: Profile,
    meta: { 
      requiresAuth: true 
    }
  }
]
```

<div class="mt-8">

## 活用例

```js
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth) {
    // 認証が必要なページの処理
    checkAuth() ? next() : next('/login')
  } else {
    next()
  }
})
```

</div>

---
transition: fade-out
---

# ネストされたルート

親子関係のあるルートを定義

<div class="grid grid-cols-2 gap-4">

<div>

## ルート定義

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

</div>

<div>

## 親コンポーネント

```vue
<template>
  <div>
    <h1>User {{ $route.params.id }}</h1>
    <nav>
      <router-link :to="`/user/${$route.params.id}/profile`">
        Profile
      </router-link>
      <router-link :to="`/user/${$route.params.id}/posts`">
        Posts
      </router-link>
    </nav>
    <router-view /> <!-- 子ルートを表示 -->
  </div>
</template>
```

</div>

</div>

---
transition: fade-out
---

# ルート遷移エフェクト

Vue の `<Transition>` を使ってアニメーションを追加

```vue {all|2-4|6-19|all}
<template>
  <router-view v-slot="{ Component }">
    <transition name="fade" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
```

<div class="mt-8 text-sm text-gray-600">

💡 `mode="out-in"` で前のコンポーネントが消えてから次が表示される  
💡 他のトランジション効果も CSS で自由に定義可能

</div>

---
transition: fade-out
---

# 実践的な例：認証付きアプリ

<div class="grid grid-cols-2 gap-4 text-sm">

<div>

## ルート設定

```js
const routes = [
  {
    path: '/',
    component: Home
  },
  {
    path: '/login',
    component: Login
  },
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

## 認証ガード

```js
router.beforeEach((to, from, next) => {
  const isLoggedIn = store.getters.isLoggedIn
  const isAdmin = store.getters.isAdmin
  
  if (to.meta.requiresAuth && !isLoggedIn) {
    next('/login')
  } else if (to.meta.requiresAdmin && !isAdmin) {
    next('/403')
  } else {
    next()
  }
})
```

</div>

</div>

---
transition: fade-out
layout: center
---

# まとめ

<div class="space-y-4 text-left max-w-2xl mx-auto">

<v-clicks>

## 📚 今日学んだこと

- Vue Router の基本的な概念とセットアップ方法
- ルート定義と動的ルーティング
- プログラムによるナビゲーション
- ナビゲーションガードによるアクセス制御
- ネストされたルートとトランジション

## ✅ できるようになったこと

- 基本的なルーティングの実装
- 動的なパラメータを使ったページ作成
- 認証が必要なページの保護

</v-clicks>

</div>

---
transition: fade-out
layout: center
---

# 次のステップ

<div class="space-y-6 text-left max-w-2xl mx-auto">

## 🎯 実践してみよう

1. **小さなプロジェクトを作る**  
   - ブログサイト（記事一覧、記事詳細、About ページ）
   - タスク管理アプリ（ログイン、ダッシュボード、タスク詳細）

2. **公式ドキュメントを読む**  
   [https://router.vuejs.org/](https://router.vuejs.org/)

3. **高度な機能を学ぶ**
   - 遅延読み込みとコード分割
   - スクロール動作のカスタマイズ
   - ルートのプリフェッチ

</div>

<div class="mt-12 text-center">
  <div class="text-2xl font-bold text-green-500">
    Happy Routing! 🚀
  </div>
</div>
