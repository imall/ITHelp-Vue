# 前言
上一篇文章，已經大概說明為什麼會需要使用框架，同時也大概說了為什麼要寫 Vue

這篇文章，來聊聊原生 JS跟 Vue 的比較吧

~~雖然上一篇好像在嘴這件事，不過這方式真的很容易能看到框架的優點~~

# Vue 幫做了什麼事情？
如果你已經有學過原生 JS 控制 Dom 的運作，那大概看得懂這段 code 在做什麼事情：

```html
<div class="message"></div>
```

```js
const $message = document.querySelector(".message");
$message.innerText = "一段文字";
```
這段原生的 JS 為了更改 HTML 節點內的資料做了兩件事： 
1. 用選取器抓到節點
2. 對這個物件設定內容


一樣的功能在 Vue 中會這樣寫：  
語法之後會再解釋，大家先注意到，在 JS 宣告的 `message` 變數可以直接寫在模板(HTML)裡面。
```html
<div id="app">
    <div>{{ message }}</div>
</div>
```
```js
Vue.createApp({
    setup() {
        const message = '一段文字'
        return { message }
    },
}).mount("#app");
```

先別嗆我說 Vue 的程式碼看起來比較多，且聽我娓娓道來...

## 指令式渲染 vs 宣告式渲染

原生JS 與 Vue 兩者所使用的思維方式不同。  
兩者對應的概念分別是為「指令式渲染」與「宣告式渲染」：

### 指令式渲染
白話來說，就是「一個口令一個動作」。  
1. 「那個誰誰誰出列！」
2. 「看到前面那棵大樹沒有？」
3. 「左去右回 20 趟，開始!!」

套用在程式上：
1. 「那個名叫 .message 的出列！」
2. 「有看到『一段文字』嗎？」  (p.s.上面例子的資料)
3. 「綁在自己身上！讓瀏覽器呈現出來！開始！」

#### 指令渲染的優點
~~優點就是我們可以當班長，命令別人做事情。~~  

直覺，我們要模板做什麼事情，儘管把他叫出來命令就是了。  
每件事情都有他的口令(語法)，只要我們能知道口令，模板就會乖乖聽話去辦事。

#### 指令渲染的缺點
如果在同一個專案中，模板要做的事情都一樣，但每次模板都在等你的口令，才知道要重複執行這個動作，你不覺得很煩嗎？

沒錯，如果網頁呈現的資料會依據使用者的操作不斷變動，要讓 HTML 重新渲染不同的資料，就必須重新叫他執行。

而且因為我們的指令同時充斥著「把人叫出來」、「叫人做事」，兩個類別的內容，如果有需要回頭改程式的時候，就必須先辨別「哪個指令是找人」、「哪個指令是做事」，無形之中其實是會消耗不少時間的！

### 宣告式渲染：
就像餐廳裏頭，各有各的任務的服務生。  
1. 「Sherry ，你顧好櫃檯」
2. 「Andy，你去負責點餐」
3. 「Eric，廚房交給你」
4. 「Patrick，收拾餐盤、洗碗就靠你了」

程式世界其實沒那麼複雜：
1. 「.title，title 變數給你渲染」
2. 「.header，header 變數給你渲染」
3. 「.content，content 變數給你渲染」
4. 「.footer，footer 變數給你渲染」  
(甚至，class 名稱都是為了符合「比喻」才要寫，實際就算沒有 class ，也可以直接叫模板綁資料。)

#### 宣告式渲染優點
就像員工教育訓練一樣，你把一個員工大概念的訓練好，未來只要類似的行為，他都知道怎麼去做。

換言之，直接透過變數綁定語法之後，我們只需要更改「變數」的資料，模板就會把資料重新渲染到瀏覽器上。

#### 宣告式渲染的缺點
相較於指令式渲染，宣告式渲染的「效能」可能會差一點點點點。

但因為現在電腦裝置效能通常都不錯，那一點點點點的差異實在是感覺不出來...
就算是手機，現在 iPhone 售價都可以買一台電腦了，他效能會不好嗎？

筆者也不確定這議題該怎麼驗證 ~~(甚至根本沒打算驗證)~~
如果有大神對此有什麼見解，也請不吝留言指教。


## 關注點分離
一份 HTML 要渲染在網頁上，通常包含兩個的資訊：
1. HTML 標籤結構，像是 div 、span 這些。
2. 資料，就是每個節點內會放的文字內容。

如果要以純 JS 的方式操控 Dom 的資料，如同上面所述，會在一支 JS 檔案中去抓節點、塞資料。

不過在宣告式渲染的模式，JS 跟模板的互動，就僅僅是把定義好的變數丟到模板中，之後就不用再管他了，就像是我們做完員工教育訓練，員工就知道自己要幹啥了。

由於模板要呈現的內容已經綁上變數，我們只要專注在「處理變數資料」，模半自動會完成渲染。

如果 PM 跑來說資料有問題，那我們就去看 JS 寫了啥，因為 JS 已經不管模板，全部都是資料的範疇，不會被「找節點的指令」所干擾。  
而如果 PM 是說畫面跑版了，那我們就回頭看 HTML 到底是哪邊寫錯。

找資料？JavaScript   
找畫面？HTML  
~~找飯店？~~ 沒...沒事...

這樣的行為，我們管他叫「關注點分離」。

## 元件化
我們開發的網站，很有可能出現好幾個「重複出現」的內容。

例如我們在逛購物網站，即使切換好幾個頁面，「頁首」跟「頁尾」基本上都是固定的。  
傳統上如果要把每一頁都實作出來，則每一個 `html` 檔案都要重複寫一次這些內容。

程式能複用，但 HTML 沒辦法。

> 工程師寫程式的最終目的，就是讓自己不要再寫程式。  By-我自己。

透過框架 (不單只 Vue，其他框架也做得到)，我們可以簡單的把這些「重複的內容」元件化，只要把資料寫一次，後續在需要的地方就可以「重複拿來使用」。

在元件的世界，不要把網頁想成「一幅畫面」，把他想成拼圖，每一塊塊的資料都是「拼圖」，在程式的世界，拼圖可以隨時被複製起來拿重複使用。   
這就是 「元件」的觀念。
![Alt text](https://i.imgur.com/TvDG8ns.png)

## 當元件的概念加上關注點分離
小朋友，你是否有很多問號？  
目前的你，可能剛學會寫好HTML結構，並且塞一些資料，讓瀏覽器呈現。  
重複使用一樣的東西，有什麼意義？

```html
<div class="card">
    <h2>小情歌</h2>
    <p>這是一首簡單的小情歌唱著人們心腸的曲折</p>
</div>
```

假設這段的內容被重複使用，畫面呈現結果可能會是這樣：
![Alt text](https://i.imgur.com/KIjqqCT.png)

顯然你已經搞懂「重複使用」的意思了，我們再把「關注點分離」的觀念帶進來：  
在框架的世界，HTML 只管「結構」，他不管「資料」，資料是 JS 的事情，不會寫在 HTML。

用這個觀念來看 HTML 跟 JS ，可能會出現這樣的語法：

```html
<div class="card">
    <h2> {{ song.name }}</h2>
    <p> {{ song.lyrics }} </p>
</div>
```

```js
const song = {
        name: "小情歌",
        lyrics: "這是一首簡單的小情歌唱著人們心腸的曲折"
    }
```

也就是說，這個 HTML 只需要寫好一次，就能當成一塊拼圖，重複在不同頁面中使用。

> 以上用一個最簡單的例子來體會元件與關注點分離的概念，不過實際的元件還可以做到更複雜的事情，之後會提到(應該)。


# 總結
框架幫助我們完成的事情

1. 宣告式渲染
2. 元件化