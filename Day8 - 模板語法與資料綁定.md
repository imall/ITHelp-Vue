# 模板語法
先說一個觀念：模板，其實不完全等於 HTML，只是剛好 Vue 使用的模板語法，完全支援 HTML。所以我們使用 Vue 的時候如果提到的「模板」，可以直接把他當成 HTML。


[Vue 官方文件](https://cn.vuejs.org/guide/essentials/template-syntax.html)的第一句話：
> Vue 使用一种基于 HTML 的模板语法，使我们能够声明式地将其组件实例的数据绑定到呈现的 DOM 上。所有的 Vue 模板都是语法层面合法的 HTML，可以被符合规范的浏览器和 HTML 解析器解析。

這段話隱含著三個觀念：
1. 我們在 Vue 實體掛載的那個 HTML 節點(`#app`)所撰寫的內容，已經不是「純」的 HTML，它只是一個「長得很像」HTML 的「模板語法」。
2. 由於語法「基於」HTML，所有 HTML 語法完全可以寫在 Vue 中。
3. 在「模板語法」中，可以透過「宣告式」的方式，把資料跟模板綁定。

怎麼宣告？雙大括號：

# Mustache 語法
Vue 支援的資料綁定語法，是透過一個叫「Mustache」的語法來處理。

這個語法的寫法很簡單，就是直接寫兩組大誇號，並且在裡面放資料，像這樣：
```html
{{ 只要會回傳一個值的資料都可以塞進來 }}
```

如果要在 HTML 標籤放資料，可以不用「只」放雙大括號，也可以把「寫死的資料」跟雙大括號結合，像這樣：

```html
<div id="app">
    <div> 歌名：{{ song }} </div>
</div>
```
```js
Vue.createApp({
    setup() {
        const song = 'あの夢をなぞって'
        return { song }
    },
}).mount("#app");

```

甚至如同 HTML 一般，我們可以不用任何標籤的包覆，即可使用雙大括號：

```html
<div id="app">
    {{ anyData }}
</div>
```
```js
Vue.createApp({
    setup() {
        const anyData = '987654321'
        return { anyData }
    },
}).mount("#app");
```


# 使用 JavaScript 表達式

在雙大擴號裡面能寫的東西，除了純粹的「變數」之外，也可以寫「JS表達式」。

換言之，只要雙大括號裡面的內容「有辦法回傳出一個值」，都是合法的資料。

例如：
```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}
```

這種寫法的好處是，我們在需要的時候可以把部分商業邏輯寫到模版裡頭。  

像是如果某個數字資料代表幣別，希望畫面上能呈現出貨幣格式，那可以這樣寫：
```html
<div id="app">
    <div> 價格： $ {{ price1.toLocaleString() }} </div>
    <div> 價格： $ {{ price2.toLocaleString() }} </div>
    <div> 價格： $ {{ price3.toLocaleString() }} </div>
</div>
```
```js
Vue.createApp({
    setup() {
        const price1 = 123456;
        const price2 = 654321;
        const price3 = 556888;
        return { price }
    },
}).mount("#app");
```



# 總結
1. Vue 使用「基於」HTML 的模板語法，只要是合法的 HTML 語法，都可以在 Vue 中撰寫。
2. Vue 的資料綁定語法使用 Mustache 語法，寫法是雙大誇號(`{{}}`)，可以單獨出現在模版中，不一定要跟 HTML 標籤寫在一起。
3. 在雙大誇號中，除了變數之外，也可以寫 JS 表達式。