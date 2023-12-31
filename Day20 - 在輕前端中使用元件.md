# 前言

雖說單一元件檔案的程式因為有 script setup 語法，能讓程式變得乾淨俐落。

不過並不是每個人都會使用 vite (或以前的 vue cli) 來使用 Vue。

用 CDN 引入 Vue 的程式開發方式，其實也能使用元件。

這篇文章要來記錄一下，這種方式使用元件的語法。

# 在輕前端使用元件

還記得可以宣告一個變數去接 `Vue.createApp` 回傳出來的東西嗎？

```js
const app = Vue.createApp({});

app.mount("#app");
```

一樣，那個 app 變數，代表能變的數 (~~好像在講廢話~~)，可以自由宣告。

而元件的定義，就是需要透過這個變數來創造：

```js
const app = Vue.createApp({});

// component 第一個參數會是元件的名字，第二個參數是物件
app.component("my-component", {});

// 內容沒打錯，本來就沒說一定要綁在 id = app 的節點。
// 我偏要綁在 class = app 的節點
app.mount(".app");
```

透過實體的 component 方法，我們可以針對這個實體去定義它的**子元件**。

記得生命週期說的嗎？

Vue 的實體本身就是一個元件，只要是元件都有它的生命週期。

用 component 定義的元件當然也不例外。

component 第一個參數是定義元件名稱，規則等等來說明，而第二個參數就是一個物件，再看一次：

```js
app.component("my-component", {});
```

而這個物件的內容可以寫的東西，就跟 createApp 中的物件完全一樣。

只不過 createApp 的模板可以直接用 #app 李面的內容取代，元件則必須寫在`template` 裡面：

```js
app.component("my-component", {
  template: `<h1> myApp：{{ data}} </h1>`,
  setup() {
    const data = Vue.ref("aaaa");
    return { data };
  },
});
```

為了方便排版，用這種模式定義的元件通常會使用 ES6 模板語法(``) 來操作。

定義好元件之後，就可以在 `#app` 中使用這個名稱：

```html
<div id="app">
  <my-component></my-component>
</div>
```

由於這個東西已經包成元件，表示它擁有重複使用的特性：

```html
<div id="app">
  <my-component></my-component>
  <my-component></my-component>
  <my-component></my-component>
</div>
```

# 元件標籤命名

一般來說，只要使用合法的 JS 屬性名稱，都可以當作 Vue 的元件名稱。

不過要知道的是，當我們建立好元件，對這個元件定義的名稱，最後是會放到 HTML 上面使用，為了避免名稱定義成跟 HTML tag 相同的字眼，通常建議以兩個以上的單字來命名。

你可能會疑惑怎麼可能定義出 HTML 標籤的名稱，標籤不都叫 `h1`、`div`、`p` 這種沒意義的字嗎？

舉例來說，我們想建立一個**對話框**的元件，於是將元件名稱定義成 `dialog`，或者我們想建立一個**跑馬燈**的元件，跑去找 google 翻譯，想知道這兩個東西的英文叫什麼，於是得到這兩個結果

![](https://i.imgur.com/QjGKipd.png)
![](https://i.imgur.com/q4jjww9.png)

於是我們就很開心的把單字寫到元件名稱中：

```js
app.component("dialog", {});
app.component("marquee", {});
```

不過你知道嗎？這兩個單字，就剛好是 HTML 中就有的標籤！
你可以點超連結進去看 MDN
[對話框](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/dialog)  
[跑馬燈](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/marquee)

雖然跑馬燈標籤 `<marquee>` 已經是官方定義不推薦使用的標籤，不過瀏覽器目前還是有支援這個標籤的運作。

我想除非真的很專精 HTML 所有標籤，否則我們很難辨別單一一個單字是不是會跟 HTML 既有標籤衝突。
最簡單的方式，就是直接使用兩個以上的單詞宣告元件名稱，例如 `<run-horse-light>` 、`<dialog-box>`。

除了這種寫法，也可以用 JS 愛用命名方式，駝峰：

```js
app.component("runHorseLight", {});
app.component("dialogBox", {});
```

在使用上，如果在 `.html` 檔案中要寫元件，必須使用連字號的寫法：

```html
<div id="app">
  <dialog-box></dialog-box>
</div>
```

如果使用駝峰寫法，.html 檔案看不懂：  
以下是**不支援**的寫法

```html
<div id="app">
  <dialogBox></dialogBox>
</div>
```


不過如果是昨天提到的 SCF  `.vue` 檔案，在 template 標籤中，這兩種寫法都可以：

```html
<template>
    <!-- 這個是 .vue 檔案中的 Template 標籤， 不是 v-if 或 v-for 使用的那個-->
  <dialog-box></dialog-box>
  <dialogBox></dialogBox>
</template>
```