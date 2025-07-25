---
theme: seriph
background: https://cover.sli.dev
title: Vue Router入門
info: |
  ## Vue Router入門
  初心者向けのVue Routerの基本概念を学ぶプレゼンテーション
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Vue Router 入門 🛣️

Vue.jsアプリケーションにルーティング機能を追加する

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer bg-white bg-opacity-10 hover:bg-opacity-20">
    Let's start our journey! <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 hover:opacity-100">
    <carbon:edit />
  </button>
  <a href="https://router.vuejs.org/" target="_blank" alt="Vue Router Docs" class="text-xl slidev-icon-btn opacity-50 hover:opacity-100">
    <carbon:logo-vue />
  </a>
</div>

<!--
このプレゼンテーションでは、Vue Routerの基本概念を初心者向けに説明します。
プログラミングとVue.jsの基本知識があることを前提としています。
-->

---
transition: fade-out
---

# Vue Routerとは？ 🤔

**Vue Router**は、Vue.jsの公式ルーターライブラリです

<v-clicks>

- 📱 **Single Page Application (SPA)** - ページ遷移を高速化
- 🧭 **ナビゲーション** - URLに基づいてコンポーネントを切り替え
- 🔗 **動的ルーティング** - パラメータ付きのURL管理
- 🛡️ **ナビゲーションガード** - アクセス制御機能

</v-clicks>

<br>

<v-click>

## なぜVue Routerが必要？

- 複数ページのWebアプリケーションを作成
- ブラウザの戻る・進むボタンに対応
- URLでページ状態を管理・共有

</v-click>

<!--
Vue RouterはVue.jsアプリでページ間の移動を管理するための公式ツールです。
従来のWebサイトとは異なり、SPAでは1つのHTMLページ内でコンテンツを動的に切り替えます。
Vue Routerがその切り替えを管理し、URLとコンポーネントを紐づけます。
-->

---
layout: two-cols
---

# 住所システムのアナロジー 🏠

Vue Routerは**郵便システム**と似ています

<v-clicks>

**郵便システム**
- 🏠 **住所** → 特定の家を特定
- 📮 **郵便配達員** → 正しい家に配達
- 🗺️ **地図** → 住所とルートの対応

**Vue Router**
- 🌐 **URL** → 特定のページを特定
- 🛣️ **Router** → 正しいコンポーネントを表示
- 📋 **Routes** → URLとコンポーネントの対応

</v-clicks>

::right::

<div v-click="4" class="mt-12">

```ts
// ルート定義 = 住所録
const routes = [
  { 
    path: '/home',      // 住所
    component: Home     // 届け先（コンポーネント）
  },
  { 
    path: '/about', 
    component: About 
  }
]
```

<div class="mt-8 p-4 bg-blue-50 rounded">
  <strong>ポイント：</strong><br>
  URLが変わると、対応するコンポーネントが表示される
</div>

</div>

<!--
このアナロジーで重要なのは、住所（URL）が変わると配達先（表示されるコンポーネント）が変わることです。
郵便配達員（Vue Router）が住所録（routes設定）を参照して、正しい場所にコンテンツを配達します。
-->

---

# セットアップ方法 🚀

Vue Routerを使い始めるための基本設定

<div class="grid grid-cols-2 gap-8">

<div>

## 1. インストール

```bash
npm install vue-router@4
```

## 2. ルーターの作成

```ts {monaco}
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'
import About from '../views/About.vue'

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
]

const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```

</div>

<div v-click>

## 3. アプリに登録

```ts {monaco}
// main.ts
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

const app = createApp(App)
app.use(router)
app.mount('#app')
```

## 4. 基本的な使用

```vue {monaco}
<!-- App.vue -->
<template>
  <div>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </nav>
    <router-view />
  </div>
</template>
```

</div>

</div>

<!--
セットアップは4つのステップです：
1. npm でパッケージをインストール
2. ルート定義とルーターインスタンスを作成
3. Vueアプリにルーターを登録
4. router-linkとrouter-viewを使ってナビゲーションを実装
-->

---
layout: two-cols
---

# 基本的なルーティング 🔗

`router-link`と`router-view`の使い方

## router-link
ナビゲーション用のリンクコンポーネント

```vue {monaco}
<template>
  <nav>
    <!-- 基本的な使用 -->
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    
    <!-- アクティブなリンクのスタイリング -->
    <router-link 
      to="/contact"
      active-class="active-link"
    >
      Contact
    </router-link>
  </nav>
</template>

<style>
.active-link {
  color: #42b883;
  font-weight: bold;
}
</style>
```

::right::

<div v-click>

## router-view
ルートに対応するコンポーネントを表示

```vue {monaco}
<template>
  <div id="app">
    <header>
      <nav>
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
      </nav>
    </header>
    
    <main>
      <!-- ここにマッチしたコンポーネントが表示される -->
      <router-view />
    </main>
  </div>
</template>
```

<div class="mt-4 p-4 bg-green-50 rounded">
  <strong>📝 覚えるポイント：</strong><br>
  • <code>router-link</code> = ナビゲーションリンク<br>
  • <code>router-view</code> = コンテンツ表示エリア
</div>

</div>

<!--
router-linkは<a>タグの代わりに使います。toプロパティで遷移先を指定します。
router-viewは現在のルートに対応するコンポーネントをレンダリングする場所です。
active-classでアクティブなリンクにスタイルを適用できます。
-->

---

# 動的ルーティング 🎯

URLパラメータを使って動的なルートを作成

<div class="grid grid-cols-2 gap-6">

<div>

## ルート定義

```ts {monaco}
// router/index.ts
const routes = [
  // 静的ルート
  { path: '/users', component: UserList },
  
  // 動的ルート（パラメータ付き）
  { 
    path: '/users/:id', 
    component: UserDetail 
  },
  
  // 複数パラメータ
  { 
    path: '/users/:id/posts/:postId', 
    component: UserPost 
  }
]
```

## ナビゲーション

```vue {monaco}
<template>
  <div>
    <!-- 静的リンク -->
    <router-link to="/users">全ユーザー</router-link>
    
    <!-- 動的リンク -->
    <router-link to="/users/123">ユーザー123</router-link>
    <router-link to="/users/456">ユーザー456</router-link>
  </div>
</template>
```

</div>

<div v-click>

## パラメータの取得

```vue {monaco}
<!-- UserDetail.vue -->
<template>
  <div>
    <h1>ユーザー詳細</h1>
    <p>ユーザーID: {{ userId }}</p>
    <p>投稿ID: {{ postId }}</p>
  </div>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'
import { computed } from 'vue'

const route = useRoute()

// パラメータを取得
const userId = computed(() => route.params.id)
const postId = computed(() => route.params.postId)

// またはreactiveに監視
watch(() => route.params.id, (newId) => {
  console.log('ユーザーIDが変更:', newId)
})
</script>
```

<div class="mt-4 p-3 bg-blue-50 rounded text-sm">
  <strong>💡 Tips:</strong> パラメータは文字列で返されます
</div>

</div>

</div>

<!--
動的ルーティングを使うと、1つのコンポーネントで複数の似たようなページを処理できます。
:id の部分がパラメータになり、useRoute()でアクセスできます。
パラメータが変更されても同じコンポーネントインスタンスが再利用されるため、watchでの監視が重要です。
-->

---

# ネストされたルート 🏗️

親子関係のあるルートを定義

<div class="grid grid-cols-2 gap-6">

<div>

## ルート構造

```ts {monaco}
// router/index.ts
const routes = [
  {
    path: '/user/:id',
    component: User,
    children: [
      // /user/:id にマッチした時は空のrouter-viewが表示
      { path: '', component: UserHome },
      
      // /user/:id/profile にマッチ
      { path: 'profile', component: UserProfile },
      
      // /user/:id/posts にマッチ
      { path: 'posts', component: UserPosts }
    ]
  }
]
```

## 親コンポーネント

```vue {monaco}
<!-- User.vue -->
<template>
  <div>
    <h1>ユーザー: {{ $route.params.id }}</h1>
    
    <nav>
      <router-link :to="`/user/${$route.params.id}`">
        ホーム
      </router-link>
      <router-link :to="`/user/${$route.params.id}/profile`">
        プロフィール
      </router-link>
      <router-link :to="`/user/${$route.params.id}/posts`">
        投稿
      </router-link>
    </nav>
    
    <!-- 子ルートがここに表示される -->
    <router-view />
  </div>
</template>
```

</div>

<div v-click>

## 子コンポーネント

```vue {monaco}
<!-- UserProfile.vue -->
<template>
  <div>
    <h2>プロフィール</h2>
    <p>ユーザーID: {{ $route.params.id }}</p>
    <!-- プロフィール情報 -->
  </div>
</template>
```

```vue {monaco}
<!-- UserPosts.vue -->
<template>
  <div>
    <h2>投稿一覧</h2>
    <p>ユーザーID: {{ $route.params.id }}</p>
    <!-- 投稿リスト -->
  </div>
</template>
```

<div class="mt-4 p-4 bg-yellow-50 rounded">
  <strong>🌳 構造のイメージ：</strong><br>
  <code>/user/123</code> → UserHome<br>
  <code>/user/123/profile</code> → UserProfile<br>
  <code>/user/123/posts</code> → UserPosts
</div>

</div>

</div>

<!--
ネストされたルートを使うと、共通のレイアウト（ヘッダーやナビゲーション）を持ちながら、
内容部分だけを切り替えることができます。
親コンポーネントのrouter-viewに子コンポーネントが表示されます。
URLの階層構造とコンポーネントの階層構造が対応します。
-->

---

# プログラムによるナビゲーション 🧭

JavaScriptコードでページ遷移を制御

<div class="grid grid-cols-2 gap-6">

<div>

## 基本的なナビゲーション

```ts {monaco}
import { useRouter } from 'vue-router'

export default {
  setup() {
    const router = useRouter()

    const goToUser = (userId: string) => {
      // 新しいエントリをhistoryスタックに追加
      router.push(`/users/${userId}`)
    }

    const goBack = () => {
      // ブラウザの戻るボタンと同じ
      router.go(-1)
    }

    const replaceRoute = () => {
      // 現在のエントリを置き換え（戻れない）
      router.replace('/dashboard')
    }

    return {
      goToUser,
      goBack,
      replaceRoute
    }
  }
}
```

</div>

<div v-click>

## 実用的な例

```vue {monaco}
<!-- Login.vue -->
<template>
  <form @submit.prevent="login">
    <input v-model="username" placeholder="ユーザー名">
    <input v-model="password" type="password" placeholder="パスワード">
    <button type="submit">ログイン</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const username = ref('')
const password = ref('')

const login = async () => {
  try {
    await authenticateUser(username.value, password.value)
    
    // ログイン成功後、ダッシュボードへリダイレクト
    router.push('/dashboard')
  } catch (error) {
    console.error('ログイン失敗:', error)
  }
}
</script>
```

<div class="mt-4 p-3 bg-green-50 rounded text-sm">
  <strong>🔄 メソッドの違い:</strong><br>
  • <code>push()</code> - 履歴に追加（戻れる）<br>
  • <code>replace()</code> - 履歴を置換（戻れない）<br>
  • <code>go(n)</code> - n個前/後に移動
</div>

</div>

</div>

<!--
プログラムによるナビゲーションは、ユーザーのアクションに応じてページ遷移を制御する際に使います。
ログイン後のリダイレクト、フォーム送信後の遷移、条件付きナビゲーションなどで活用します。
pushとreplaceの違いを理解することが重要です。
-->

---

# ナビゲーションガード 🛡️

ページ遷移時のアクセス制御

<div class="grid grid-cols-2 gap-6">

<div>

## グローバルなガード

```ts {monaco}
// router/index.ts
import { createRouter } from 'vue-router'

const router = createRouter({
  // ...routes
})

// 全ての遷移前に実行
router.beforeEach((to, from, next) => {
  // 認証が必要なページの場合
  if (to.meta.requiresAuth) {
    if (!isAuthenticated()) {
      // ログインページにリダイレクト
      next('/login')
    } else {
      next() // 遷移を許可
    }
  } else {
    next() // 遷移を許可
  }
})

// ルート定義（メタフィールド付き）
const routes = [
  {
    path: '/dashboard',
    component: Dashboard,
    meta: { requiresAuth: true }
  },
  {
    path: '/login',
    component: Login
  }
]
```

</div>

<div v-click>

## コンポーネント内ガード

```vue {monaco}
<!-- UserEdit.vue -->
<template>
  <form @submit.prevent="save">
    <input v-model="userData.name" placeholder="名前">
    <button type="submit">保存</button>
  </form>
</template>

<script setup lang="ts">
import { ref, onBeforeRouteLeave } from 'vue-router'

const userData = ref({ name: '' })
const hasUnsavedChanges = ref(false)

// フォームの変更を監視
watch(userData, () => {
  hasUnsavedChanges.value = true
}, { deep: true })

// ページを離れる前に確認
onBeforeRouteLeave((to, from, next) => {
  if (hasUnsavedChanges.value) {
    const answer = window.confirm(
      '未保存の変更があります。本当に離れますか？'
    )
    if (answer) {
      next()
    } else {
      next(false) // 遷移をキャンセル
    }
  } else {
    next()
  }
})
</script>
```

<div class="mt-4 p-3 bg-red-50 rounded text-sm">
  <strong>⚠️ 注意:</strong> <code>next()</code>を必ず呼ぶこと
</div>

</div>

</div>

<!--
ナビゲーションガードはセキュリティとユーザビリティの両方で重要です。
beforeEach はログイン認証、権限チェックに使います。
onBeforeRouteLeave は未保存データの確認、重要な処理の中断防止に使います。
next()を呼び忘れると遷移が止まってしまうので注意が必要です。
-->

---
layout: center
class: text-center
---

# まとめ & 次のステップ 🎯

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

## 今日学んだこと ✅

<v-clicks>

- Vue Routerの基本概念と役割
- セットアップと基本設定
- router-link と router-view の使い方
- 動的ルーティング（パラメータ）
- ネストされたルート（親子関係）
- プログラムによるナビゲーション
- ナビゲーションガード（アクセス制御）

</v-clicks>

</div>

<div v-click="8">

## 次のステップ 🚀

### さらに学ぶべき内容
- 遅延ローディング（Lazy Loading）
- スクロール動作のカスタマイズ
- トランジション/アニメーション
- 高度なナビゲーションガード

### リソース 📚
- [Vue Router公式ドキュメント](https://router.vuejs.org/)
- [Vue.js公式ガイド](https://vuejs.org/guide/)
- [実践的なサンプルコード](https://github.com/vuejs/router)

</div>

</div>

<div v-click="9" class="mt-12 p-6 bg-green-50 rounded-lg">
  <h3 class="text-xl font-bold mb-4">🎉 お疲れさまでした！</h3>
  <p>Vue Routerの基礎をマスターしたあなたは、本格的なVue.jsアプリケーションを作る準備ができています。</p>
</div>

<!--
このプレゼンテーションでVue Routerの基本的な概念を網羅しました。
実際のプロジェクトでは、これらの機能を組み合わせて使うことが多いです。
まずは小さなプロジェクトから始めて、徐々に複雑な機能を追加していきましょう。
公式ドキュメントは常に最新の情報を提供しているので、困った時は参照してください。
-->