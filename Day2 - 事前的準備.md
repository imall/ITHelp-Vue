# 事前的準備

工欲善其事，必先利其器。  

這句不知道已經幾百年的諺語一直到現在還是很受用，我們學習程式的人也適用於這個觀念。  

開始學習 Vue 之前，有幾樣工具是電腦中一定要準備好的。


# Visual Studio Code
[Visual Studio Code](https://code.visualstudio.com/download)

我認識寫前端程式的人，清一色都是用這個 IDE，甚至此刻你在讀的這篇文章也是在 VSCode 寫出來的，所以我也推薦剛入門的新手，透過這個 IDE 來學習程式。

Visual Studio Code 安裝方式基本上依照網站上的指示下載安裝即可。  
如果是 Windows 的使用者，建議安裝到這步時，把「其他」的四個選項全部打勾。  
![vscode](https://i.imgur.com/2njc0RF.jpg)

## 擴充套件

`Visual Studio Code` 最厲害的功能，就是我們可以使用大神們開發出來的外掛，可以在左邊那欄選單找到這顆按鈕安裝。  
![Alt text](https://i.imgur.com/qkWeigZ.png)

推薦幾個適合開發的套件，以及開發 Vue 官方建議安裝的工具：

1. [Chinese (Traditional) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hant)：
如果你對英文感到畏懼，這個工具很適合你，他可以直接讓我們的 VScode 中文化。


2. [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)：
一個能幫我們排版程式碼的工具。


3. [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)：
這個套件能幫我們起一個簡單的伺服器，來預覽 HTML 在瀏覽器呈現的畫面。同時支援 「熱重載」<sup>註1</sup> ，讓我們可以在更改檔案當下，及時把資料重新「渲染」<sup>註2</sup>到瀏覽器的畫面上。

4. [Vue Language Features (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.volar)：Vue 開發者必裝套件。  
未來我們會面對一個附檔名叫 `.vue` 的檔案，這是 Vue 框架才會出現的東西。  
因為 VScode 看不懂這個檔案的語法，會一直報「語法錯誤」的提示，這會讓人誤會自己的 Code 是不是有寫錯。   
Vue 團隊為了提升 DX <sup>註3</sup>，提供 Volar 套件來處理這個問題。  
簡單來說，如果你要深入使用 Vue 這個框架，那 Volar 會是你必裝的套件之一。


> 註
> 1. 熱重載(Hot Reload)：自動讓瀏覽器重新渲染的功能，可以節省我們手動點擊「重新整理」的時間，之後會介紹到的 `vite` 也會有這樣的特性。
> 
> 2. 渲染：意思是把我們寫出來的「HTML」或是「JS 程式」在瀏覽器中「畫」出畫面的過程。
上面提到的「重新渲染」，意思則是瀏覽器重新「畫」了畫面的行為。
> 
> 3. DX (Developer Experience)：開發者體驗。過往程式開發都在追求使用者體驗，比較少會有人在意開發者寫程式過程是否感到友善，不過 Vue 團隊會為此特別琢磨，希望 Vue 開發者能在開發過程更順利。  

# Vue 的開發者工具 (Chrome 的擴充套件)
[Vue.js devTools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)


Vue 其實是個很在乎開發者體驗的團隊，為了讓開發人員更舒服，他們一直有在調整 Vue 生態圈提供的開發工具以及開發模式，其中包含語法的改變、外掛的應用。  

這裡請大家安裝的 Chrome 擴充套件： Vue 開發者工具，是一個 Vue2 時代就有的產物，過程經歷一個改版，目前都是建議安裝新版的 Vue 開發者工具。

這個工具可以讓我們在開發過程中，更好追蹤 Vue 元件的狀態、Pinia 設定的資料。

> 關於 `元件`、`狀態`、`Pinia` ，這些以後會專門寫一篇文章來跟大家講解。


# Node.js

[Node.js](https://nodejs.org/zh-tw)

如果你還沒踏入 JavaScript 的世界，~~那麼快逃~~，那麼你可能還不知道 Node.js 是什麼東西。
 
首先要知道，JS 其實是設計來在瀏覽器運行的程式語言，換句話說，在那些沒有 Node.js 的日子，只要離開瀏覽器，就沒辦法執行 JS 程式。

可能是因為 JS 太好用，所以有位技術大神 Rayn Dahl 就發明出 Node.js 這套工具，讓 JS 即使脫離瀏覽器也能在這個「環境」執行 JavaScript。

那所以這個環境在哪裡？  
在我們安裝 Node.js 的過程中，就會幫我們把這個「環境」設定在我們的電腦系統內(Windows 叫環境變數，Mac 我不知道)，使我們不用透過瀏覽器，也可以在「本機」執行 JS 。

但這東西跟 Vue ，跟前端有什麼關係，我們寫 Vue 不就是要讓 JavaScript 在瀏覽器上執行嗎？  
這個觀念沒錯，Vue.js 的底層 是 JavaScript ，並且我們學習 Vue 的最終目的，也是要讓瀏覽器執行我們寫的 Vue。

會用到 Node.js ，更準確的說，是為了能使用各路大神們開發好的「程式工具包」，我們會用 [npm (Node Package Manager)](https://www.npmjs.com/) 來安裝這些工具包 <sup>註1</sup> 。  

npm 的中文翻譯是 Node 套件管理器，同時也是 Node.js 預設供開發者管理套件的工具，它在我們安裝 Node.js 時會一併被安裝。

而部分的工具在運行的過程，會需要用到本機的 JS 環境：Node，例如之後(應該)會寫的 Vite 就是一個例子。

> 註 1： 除了 `npm` 之外，其他還有像 `yarn` 、`pnpm` 等套件管理工具都可以安裝 Node.js 套件。

---
以上的所有內容都準備好之後，下一篇文章開始，準備來認識 Vue 吧。