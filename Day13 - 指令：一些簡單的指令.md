# 指令介紹
開始進入指令的章節，先前有提到，在 Vue 中，只要看到 `v-` 開頭的東西，就是指令。

指令的用途很多，例如：資料綁定、事件綁定、條件判斷、迴圈等等。

而只要是指令，都會是寫在 HTML 標籤的「屬性」中，像這樣：

```html
<div v-if="isShow">我會顯示嗎？</div>
```

如同 HTML 屬性一樣，指令可以單獨出現，也會有不用帶「屬性值」的指令，像這樣：
```html
<span v-once>This will never change: {{msg}}</span>
```

大致了解之後，先來介紹一些我「很少用」的指令當開端   
~~(感覺如果最後才介紹，應該一下就忘記了XD)~~

# 一些簡單的指令
## v-text
這個指令用來將變數資料塞到 HTML 標籤中，底層的原理是使用 [textContent](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent) 來實現的，所以他會直接覆蓋整個標籤的所有內容。

所以當 HTML 寫上 `v-text` ，就如同 HTML 內只寫 「雙大括號」一樣：
```html
<span v-text="msg"></span>
<!-- 等同於 -->
<span>{{msg}}</span>
```

不過由於 `v-text` 是直接覆蓋「所有內容」，用法就沒有雙大括號來得彈性。  
在雙大括號中，還可以在添加一些額外的資料，但 `v-text` 沒辦法，這也是我不太常使用它的原因。

```html
<span>這是一個訊息：{{msg}}</span>

<span v-text="msg">這裡寫的內容都會被覆蓋掉，沒辦法顯示</span>
```


## v-html
這個指令其實跟 `v-text` 用法一樣，都是會抽換掉整個 HTML 標籤內的內容。
唯一不同的是，`v-html` 會把資料當成 HTML 來解析，而不是純文字。

```html
<span v-html="msg"></span>
```

```js
const app = Vue.createApp({
    setup(){
        const msg = '<span style="color:red">這是一個紅色的文字</span>'
        return { msg }
    }
})
``` 

如果用 `v-text` 的話，會直接把 msg 裡面的資料視為純文字。

不過使用 `v-html` 的話，資料內容有 HTML 標籤，是會直接被解析成 HTML 的。

## v-once
這個指令用來讓某個 HTML 節點所綁定的資料，只被渲染一次。

舉例來說，如果我們有一個資料叫做 `msg`，並且在 HTML 中使用 `v-once` 綁定，那麼這個資料只會被渲染一次。

```html
<span v-once @click="plus">{{number}}</span>
```

```js
const app = Vue.createApp({
    setup(){
        const number = ref(0)
        const plus = ()=>{
             number.value++
            console.log(number.value)
           
        }
        return { number,plus }
    }
}).mount('#app')
```

像是[這個例子](https://jsfiddle.net/imall/q6btwn4a/10/)，點擊 `span` 時，其實資料持續都有被更動，但畫面就只會只會呈現第一次。

能想到一個使用情境是，如果我們希望某個資料維持初始值不要被更動，就可以先用 v-once 綁在某個節點上，像是[這個範例](https://jsfiddle.net/imall/q6btwn4a/7/)

## v-pre
`v-pre` 基本上就....更不會用到了....  
他可以用來「不要讓 {{}}」被 Vue 解析，而是直接顯示出來。

```html
<span v-pre>{{ 1 + 1}}</span>
```

呈現結果[在這](https://jsfiddle.net/imall/q6btwn4a/14/)


# 總結
1. 指令都是寫在 HTML 標籤的屬性中，並且以 `v-` 開頭。
2. 指令可以單獨出現，也可以有「屬性值」。
3. `v-once` 指令讓模版只對資料綁定一次
4. `v-text` 指令會直接覆蓋整個標籤的所有內容。
5. `v-html` 指令會把資料當成 HTML 來解析，而不是純文字。
6. `v-pre`  指令可以用來「不要讓 `{{}}` 被 Vue 解析」，而是直接顯示出來。