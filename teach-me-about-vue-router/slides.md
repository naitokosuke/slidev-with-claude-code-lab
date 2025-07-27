---
theme: seriph
# より読みやすいシンプルな背景に変更
background: '#1e3a8a'
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

<div class="text-center mt-16">

## **Vue.jsで「ページ遷移」を実現する公式ライブラリ**

<div class="mt-16 text-2xl">

🔗 **URLでページを切り替え**

<div class="mt-8 text-xl text-gray-300">
<code class="bg-blue-900 px-4 py-2 rounded text-white">/home</code> → ホームページ<br><br>
<code class="bg-blue-900 px-4 py-2 rounded text-white">/about</code> → アバウトページ
</div>

</div>

</div>

<!--
Vue RouterはVue.jsアプリでページ間の移動を管理するための公式ツールです。
従来のWebサイトとは異なり、SPAでは1つのHTMLページ内でコンテンツを動的に切り替えます。
Vue Routerがその切り替えを管理し、URLとコンポーネントを紐づけます。
-->

---

# なぜVue Routerが必要？ 🤔

<div class="text-center mt-12">

## **普通のVue.jsだけでは...**

<div class="mt-12 text-2xl space-y-6">

❌ ページ遷移ができない

❌ URLが変わらない

❌ ブラウザの戻るボタンが使えない

</div>

<div class="mt-16 p-8 bg-green-800 text-white rounded-lg text-2xl">
✨ **Vue Routerですべて解決！**
</div>

</div>

---

# 簡単な例で理解しよう 🏠

<div class="text-center mt-12">

## **Vue Router = 「住所」と「家」を繋ぐシステム**

<div class="mt-16 text-xl space-y-8">

<div class="p-8 bg-blue-900 text-white rounded border">
  <h3 class="text-2xl font-bold mb-4">🏠 現実世界</h3>
  <p class="text-xl">「東京都渋谷区...」の住所 → 特定の家に到着</p>
</div>

<div class="p-8 bg-green-800 text-white rounded border">
  <h3 class="text-2xl font-bold mb-4">🌐 Vue Router</h3>
  <p class="text-xl">「/home」のURL → ホームコンポーネントを表示</p>
</div>

</div>

</div>

<!--
このアナロジーで重要なのは、住所（URL）が変わると配達先（表示されるコンポーネント）が変わることです。
郵便配達員（Vue Router）が住所録（routes設定）を参照して、正しい場所にコンテンツを配達します。
-->

---

# セットアップ: 1. インストール 📦

<div class="text-center mt-16">

## **Vue Routerをプロジェクトに追加**

<div class="mt-16">

### プロジェクトのルートディレクトリで実行：

```bash
npm install vue-router@4
```

<div class="mt-12 p-6 bg-green-800 text-white rounded text-xl">
✅ これでVue Routerがプロジェクトに追加されました！
</div>

</div>

</div>

---

# セットアップ: 2. ルート定義 🗺️

<div class="mt-8">

## **`router/index.ts` でルートを定義**

```ts
// router/index.ts
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
]
```

<div class="mt-8 p-6 bg-blue-900 text-white rounded text-lg">
💡 **ポイント**: URLとコンポーネントを対応付け
</div>

</div>

---

# セットアップ: 3. ルーター作成 ⚙️

<div class="mt-8">

## **ルーターインスタンスを作成**

```ts
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(),
  routes
})
```

</div>

---

# セットアップ: 4. アプリ登録 🔗

<div class="mt-8">

## **Vueアプリにルーターを登録**

```ts
// main.ts
import { createApp } from 'vue'
import router from './router'

const app = createApp(App)
app.use(router)
```

</div>

---

# セットアップ: 5. テンプレート使用 🎨

<div class="mt-8">

## **`router-view`でコンテンツ表示**

```vue
<!-- App.vue -->
<template>
  <div>
    <router-view />
  </div>
</template>
```

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

# セットアップ: 6. ナビゲーションリンク 🔗

<div class="mt-8">

## **`router-link`でページ遷移**

```vue
<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </nav>
</template>
```

<div class="mt-8 p-6 bg-green-800 text-white rounded text-lg">
✨ **完成！** これでVue Routerが使えるようになりました
</div>

</div>

<!--
router-linkは<a>タグの代わりに使います。toプロパティで遷移先を指定します。
router-viewは現在のルートに対応するコンポーネントをレンダリングする場所です。
active-classでアクティブなリンクにスタイルを適用できます。
-->

---

# 動的ルーティングとは？ 🎯

<div class="text-center mt-12">

## **1つのコンポーネントで複数の似たページを処理**

<div class="mt-16 text-xl">

例：「ユーザー123の詳細」「ユーザー456の詳細」などを
同じコンポーネントで処理できます

</div>

<div class="mt-12 p-8 bg-blue-900 text-white rounded border text-xl">
<code class="bg-blue-800 px-3 py-1 rounded">/users/123</code> → UserDetailコンポーネント<br><br>
<code class="bg-blue-800 px-3 py-1 rounded">/users/456</code> → 同じUserDetailコンポーネント
</div>

</div>

---

# 動的ルートの定義 📋

## **`:id` でパラメータを指定**

```ts
// router/index.ts
const routes = [
  { path: '/users/:id', component: UserDetail }
]
```

---

# パラメータの仕組み 🔑

## **`:id` の部分が動的に変わります**

<div class="mt-8 space-y-4 text-xl">

✅ `/users/123` → `id = "123"`

✅ `/users/456` → `id = "456"`

✅ `/users/abc` → `id = "abc"`

</div>

<div class="mt-8 p-6 bg-blue-900 text-white rounded border text-lg">
💡 **すべて同じUserDetailコンポーネントで処理**
</div>

---

# パラメータの取得 (1/2) 📝

## **`useRoute`を使ってアクセス**

```vue
<script setup lang="ts">
import { useRoute } from 'vue-router'

const route = useRoute()
</script>
```

---

# パラメータの取得 (2/2) 📝

## **パラメータを取得**

```vue
<script setup lang="ts">
const userId = computed(() => route.params.id)
</script>

<template>
  <p>ユーザーID: {{ userId }}</p>
</template>
```

<div class="mt-8 p-6 bg-blue-900 text-white rounded border text-lg">
💡 **重要**: パラメータはすべて文字列で返されます
</div>

<!--
動的ルーティングを使うと、1つのコンポーネントで複数の似たようなページを処理できます。
:id の部分がパラメータになり、useRoute()でアクセスできます。
パラメータが変更されても同じコンポーネントインスタンスが再利用されるため、watchでの監視が重要です。
-->

---

# ネストされたルート 🏗️

<div class="grid grid-cols-2 gap-8">

<div>

```ts
const routes = [{
  path: '/user/:id',
  component: User,
  children: [
    { path: '', component: UserHome },
    { path: 'profile', component: UserProfile },
    { path: 'posts', component: UserPosts }
  ]
}]
```

</div>

<div>

## ポイント

**メリット**
- 共通部分を1度だけ書く
- URLが階層的になる

**使用例**
- `/user/123` → 基本情報
- `/user/123/profile` → 詳細
- `/user/123/posts` → 投稿

</div>

</div>

---

# 親コンポーネント: ナビゲーション 🧭

```vue
<!-- User.vue template部分 -->
<template>
  <div>
    <h1>ユーザー: {{ $route.params.id }}</h1>
    
    <nav>
      <router-link :to="`/user/${$route.params.id}`">
        ホーム
      </router-link>
    </nav>
  </div>
</template>
```

---

# 親コンポーネント: router-view 📺

```vue
<!-- User.vue template部分 -->
<template>
  <div>
    <!-- ナビゲーション -->
    
    <!-- 子ルートがここに表示される -->
    <router-view />
  </div>
</template>
```

<div class="mt-8 p-6 bg-blue-900 text-white rounded border text-lg">
💡 **`router-view`に子コンポーネントが表示される**
</div>

---

# 子コンポーネント例 🔄

## UserProfile.vue

```vue
<!-- UserProfile.vue -->
<template>
  <div>
    <h2>プロフィール</h2>
    <p>ユーザーID: {{ $route.params.id }}</p>
  </div>
</template>
```

<!--
ネストされたルートを使うと、共通のレイアウト（ヘッダーやナビゲーション）を持ちながら、
内容部分だけを切り替えることができます。
親コンポーネントのrouter-viewに子コンポーネントが表示されます。
URLの階層構造とコンポーネントの階層構造が対応します。
-->

---

# プログラムによるナビゲーション 🧭

**JavaScriptでページ遷移を制御**

フォーム送信後、ログイン成功後などに使用。

---

# 基本的なナビゲーション 📍

<div class="grid grid-cols-2 gap-8">

<div>

## コード例

```ts
import { useRouter } from 'vue-router'

const router = useRouter()

const goToUser = (userId: string) => {
  router.push(`/users/${userId}`)
}
```

</div>

<div>

## なぜ必要？

**push()の特徴**
- 履歴に追加される
- 戻るボタンが使える

**使用場面**
- ボタンクリック時
- 処理完了後の遷移

</div>

</div>

---

# ナビゲーションメソッド 🔄

<div class="grid grid-cols-2 gap-8">

<div>

## 3つのメソッド

<div class="space-y-4 text-lg">

**`push()`** - 履歴に追加  
**`replace()`** - 履歴を置換  
**`go(n)`** - n個前/後に移動

</div>

</div>

<div>

## いつ使う？

**push()** → 通常の画面遷移

**replace()** → ログイン後など

**go(-1)** → 戻るボタン

</div>

</div>

---

# ログインフォーム例 📝

```vue
<!-- Login.vue template -->
<template>
  <form @submit.prevent="login">
    <input v-model="username" placeholder="ユーザー名">
    <button type="submit">ログイン</button>
  </form>
</template>
```

---

# ログイン処理例 🔑

```vue
<!-- Login.vue script -->
<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const login = async () => {
  await authenticateUser()
  router.push('/dashboard') // ログイン成功後リダイレクト
}
</script>
```

<!--
プログラムによるナビゲーションは、ユーザーのアクションに応じてページ遷移を制御する際に使います。
ログイン後のリダイレクト、フォーム送信後の遷移、条件付きナビゲーションなどで活用します。
pushとreplaceの違いを理解することが重要です。
-->

---

# ナビゲーションガードとは 🛡️

**ページ遷移の前後に実行されるセキュリティチェック**

アクセス制御（ログイン確認、権限チェック）やユーザビリティ向上（未保存データの確認）に使用します。

---

# グローバルなガード 🌐

<div class="grid grid-cols-2 gap-8">

<div>

## コード例

```ts
// router/index.ts
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth) {
    if (!isAuthenticated()) {
      next('/login')
    } else {
      next()
    }
  } else {
    next()
  }
})
```

</div>

<div>

## 重要ポイント

**いつ実行される？**
- 全ページ遷移時

**パラメータ**
- `to`: 行き先
- `from`: 元の場所
- `next`: 許可/拒否

⚠️ **next()は必須！**

</div>

</div>

---

# コンポーネント内ガード: フォーム 📝

```vue
<!-- UserEdit.vue template -->
<template>
  <form @submit.prevent="save">
    <input v-model="userData.name" placeholder="名前">
    <button type="submit">保存</button>
  </form>
</template>
```

---

# コンポーネント内ガード: 確認処理 🔒

```vue
<!-- UserEdit.vue script -->
<script setup lang="ts">
import { onBeforeRouteLeave } from 'vue-router'

onBeforeRouteLeave((to, from, next) => {
  if (hasUnsavedChanges.value) {
    const answer = window.confirm('未保存データがあります')
    next(answer)
  } else {
    next()
  }
})
</script>
```

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

# 今日学んだこと (1/2) ✅

<div class="text-center mt-12">

## **Vue Routerの基本をマスターしました！**

<div class="mt-16 text-2xl space-y-6">

✅ Vue Routerの基本概念と役割

✅ セットアップと基本設定

✅ router-link と router-view の使い方

</div>

</div>

---

# 今日学んだこと (2/2) ✅

<div class="text-center mt-12">

<div class="mt-16 text-2xl space-y-6">

✅ 動的ルーティング（パラメータ）

✅ ネストされたルート

✅ プログラムによるナビゲーション

✅ ナビゲーションガード

</div>

</div>

---

# 次のステップ 🚀

<div class="text-center mt-16">

## **さらに学ぶべき内容**

<div class="text-2xl space-y-8">

📚 遅延ローディング（Lazy Loading）

🎨 トランジション/アニメーション

🛡️ 高度なナビゲーションガード

</div>

</div>

---

# 参考リソース 📚

<div class="text-center mt-16">

## **さらに学習を続けるために**

<div class="mt-16 space-y-6">

<div class="p-6 bg-blue-900 text-white rounded border">
  <h3 class="text-xl font-bold mb-2">📝 Vue Router公式ドキュメント</h3>
  <p class="text-lg">https://router.vuejs.org/</p>
</div>

<div class="p-6 bg-green-800 text-white rounded border">
  <h3 class="text-xl font-bold mb-2">📚 Vue.js公式ガイド</h3>
  <p class="text-lg">https://vuejs.org/guide/</p>
</div>

</div>

</div>

---
layout: center
class: text-center
---

# 🎉 お疲れさまでした！

<div class="mt-12">

## **Vue Routerの基礎をマスターしました**

<div class="mt-16 text-xl">

本格的なVue.jsアプリケーションを作る準備ができています。

<div class="mt-12 text-lg opacity-80">
小さなプロジェクトから始めて、学んだ機能を実際に使ってみましょう！
</div>

</div>

</div>

<!--
このプレゼンテーションでVue Routerの基本的な概念を網羅しました。
実際のプロジェクトでは、これらの機能を組み合わせて使うことが多いです。
まずは小さなプロジェクトから始めて、徐々に複雑な機能を追加していきましょう。
公式ドキュメントは常に最新の情報を提供しているので、困った時は参照してください。
-->