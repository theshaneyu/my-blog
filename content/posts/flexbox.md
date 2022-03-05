---
title: 'Flexbox'
date: 2022-02-15T18:33:47+08:00
draft: false
---

# 基本觀念

當我回頭看當初學習 flexbox 時，比較沒有釐清但是卻是最重要的觀念就是：**flexbox 相關的 properties 總共分成 `flex container` 與 `flex items` 兩種**

所謂 flex container 也就是包含著 flex items 的 parent elements 例如你想要針對三個 child items 在一個 parent element 中排列的方式進行設定，你可能會這樣安排你的 html

```html
<div class="flexbox-container">
  <div class="flexbox-item flexbox-item1"></div>
  <div class="flexbox-item flexbox-item2"></div>
  <div class="flexbox-item flexbox-item3"></div>
</div>
```

而 flexbox 的 properties 也就是分成專門給 `flex container` 的屬性（設定在 `flexbox-container` class）與專門給 `flex items` 的屬性（設定在 `flexbox-item1`、`flexbox-item2` 與 `flexbox-item3`）

其實 flexbox 的目的，也就是讓你能在不一個一個設定 flex item 的情況下彈性地調整 flex container 內 flex items **在一個方向上（水平或垂直）** 排列的方式

顯然這邊特別提到一個方向上，表示會有能夠在兩個方向上（水平和垂直）設定排列方式的屬性，也就是 `grid` property

# 預設值

承上方所描述的 html，今天將 `flex items` 做如下設定（省略掉一些無關的 styling）：

```css
.flexbox-item {
  width: 200px;
  margin: 10px;
  border: 3px solid #333;
  background-color: #dfdfdf;
}

.flexbox-item1 {
  min-height: 100px;
}

.flexbox-item2 {
  min-height: 200px;
}

.flexbox-item3 {
  min-height: 300px;
}
```

會得到這樣的三個高度不一樣的矩形：

![original](/flexbox/original.png)

而如果我們希望這三個 items 按照 flexbox 的方式進行排列，只要在 `flex container` 內設定：

```css
.flexbox-container {
  display: flex;
}
```

便可將三個 items 像這樣做排列：

![original](/flexbox/first-flex.png)

這邊可以發現三件事情：

1. 三個 items 呈水平方向排列
2. 三個 items 靠左排列
3. 三個不同高度的 items 變成相同的高度

這邊便會帶到後來的我希望當初學習 flexbox 時更注意的事情：**properties 的 default values**

會出現上述三個現象是因為當我們把 flex container 的 `display` 設定為 `flex` 時，該 flex container 會自動擁有一些 flexbox properties 並且將以**預設值**進行設定

1. `flex-direction` 設定為預設值 `row`，使得三個 items 呈水平排列
2. `justify-content` 設定為預設值 `flex-start`，使得三個 items 向左靠攏
3. `align-items` 預定為預設值 `stretch`，使得 item1 和 item2 被拉伸為和 item3 一樣的高度

我也將在本篇的結尾附上一些我覺得比較重要的 property 的預設值

# Flex container properties

## `justify-content` property

CSS styling 當中最常做的事情莫過於將一個 element **水平置中**，此時我們可以透過對 flex container 設定 `justify-content: center` 來達到水平置中

```css
.flexbox-container {
  display: flex;
  justify-content: center;
}
```

![justify-center](/flexbox/justify-center.png)

將 justify-content 設定為 `center` 後，所有 items 將會被擠到中間，且彼此之間不會預留空間（此處的空隙是因為 `flexbox-item` class 有設定 margin）

如果你希望在 items 之間盡可能地塞滿空間，可以將 justify-content 設定為 `space-between`

```css
.flexbox-container {
  display: flex;
  justify-content: space-between;
}
```

![justify-between](/flexbox/justify-between.png)

如果希望將 items 之間的空間平均地分配到 items 的兩邊，可以使用 `space-around`

```css
.flexbox-container {
  display: flex;
  justify-content: space-around;
}
```

![justify-around](/flexbox/justify-around.png)

## `align-items` property

如剛才所提到的，一但將 flex container 設定為 `display:flex`，三個 items 的高度都將會變成一樣，是因為 `align-items` 的預設值為 `stretch`，而如果將 `align-items` 設定為 `flex-start`，則三個 items 的高度將會回到原本的值，並且朝上靠攏

```css
.flexbox-container {
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
}
```

![align-start](/flexbox/align-start.png)

而另外一個在 css styling 中最常做的事情便是**垂直置中**，而這個可以透過將 align-items 設定為 `center` 來達到，在 flexbox 推出之前，要將 element 做垂直置中幾乎是不可能的事

```css
.flexbox-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
```

![align-center](/flexbox/align-center.png)

## `align-content` property

另一個不是很常用的 property 是 `align-content` property，align-content property 只會在多行的 flex items 中使用

如果我們將視窗的寬度縮窄，增加 flex container 的高度，並且將 flex container 的 `flex-wrap` 設定為 `wrap`，則 flex items 將呈 multi-line 排列

```css
.flexbox-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 700px;
  flex-wrap: wrap;
}
```

![flex-wrap](/flexbox/flex-wrap.png)

而如果我們再將 `align-content` 設定為 `flex-start`，則這些 multi-line 的 items 將會在各自的 row 向上靠攏

```css
.flexbox-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 700px;
  flex-wrap: wrap;
  align-content: flex-start;
}
```

![align-content-start](/flexbox/align-content-start.png)

`align-content` 不是一個經常使用的 property，其實大部分的時間只要使用 `jutify-content` 和 `align-items` 就可以分別在水平和垂直方向進行排列

## `flex-direction` property

如同上面提到的，`flex-direction` 的預設值為 `row`，而如果我們將之設定為 `column`，並設定 `jutify-content: center`

```css
.flexbox-container {
  height: 800px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
```

![direction-column](/flexbox/direction-column.png)

可以看到 `justify-content` 不再以水平方向作用，而是改以垂直方向來產生 `center` 的效果

# Flex items properties

Flex items 的 properties 用於設定某特定 flex item 的尺寸及排列方式等等

## `flex-shrink` property

預設情況下，如果我們將瀏覽器視窗的寬度縮小至小於 flex container 的寬度時，flexbox 會自動將每個 flex items 的寬度縮小

![width](/flexbox/width.png)

![width-shrink](/flexbox/width-shrink.png)

而如果我們希望 item1 永遠保值原本的寬度而不要被縮小，則可以針對 item1 設定 `flex-shrink: 0`

```css
.flexbox-item-1 {
  min-height: 100px;
  flex-shrink: 0;
}
```

![shrink-0](/flexbox/shrink-0.png)

## `flex-grow` property

如果我們希望在 flex container 的寬度增加時，讓 item3 的寬度也隨之增加，並填滿所有剩餘的空間，可以設定 `flex-grow: 1`

```css
.flexbox-item-3 {
  min-height: 300px;
  flex-grow: 1;
}
```

![flex-grow](/flexbox/flex-grow.png)

如果我們將 item2 也設定 `flex-grow: 1`，則 item2 和 item3 將會平分所有剩餘的空間

```css
.flexbox-item-2 {
  min-height: 200px;
  flex-grow: 1;
}

.flexbox-item-3 {
  min-height: 300px;
  flex-grow: 1;
}
```

![flex-grow-2](/flexbox/flex-grow-2.png)

如果我們將 item2 設定為 `flex-row: 2` 並將 item1 設定為 `flex-grow: 1`，則 flexbox 會將 container 的所有剩餘空間，以 2:1 的方式增加到 item2 和 item3 上面

此處需特別注意，**item2 的寬度並不會剛好是 item3 的兩倍**，因為他們兩個各自都有原本的寬度，flexbox 只是將剩餘的空間以 2:1 的比例加到他們兩個上面而已

```css
.flexbox-item-2 {
  min-height: 200px;
  flex-grow: 2;
}

.flexbox-item-3 {
  min-height: 300px;
  flex-grow: 1;
}
```

![flex-grow-3](/flexbox/flex-grow-3.png)

如果我們希望 item2 的寬度剛好是 item3 的兩倍，可以把兩個 items 都設定 `flex-basic: 0`，如此一來 flexbox 便會假設 item2 和 item3 的原始寬度都是 0，然後再將剩餘的空間以 2:1 的比例分配給 item2 和 item3

```css
.flexbox-item-2 {
  min-height: 200px;
  flex-grow: 2;
  flex-basis: 0;
}

.flexbox-item-3 {
  min-height: 300px;
  flex-grow: 1;
  flex-basis: 0;
}
```

![flex-grow-4](/flexbox/flex-grow-4.png)

## `align-self` property

align-self property 用於設定單一 flex item 於垂直方向對齊的方式例如如果我們將 item2 設定 `align-self: center`，則 item2 將會回復到原本的高度（item2 原本個高度是 200px，會被拉伸成 300px 是因為 flex container 的 align-items 值預設為 `stretch`），並且垂直置中

```css
.flexbox-item-2 {
  min-height: 200px;
  flex-grow: 2;
  flex-basis: 0;
  align-self: center;
}
```

![align-self](/flexbox/align-self.png)

以上大概就是我認為比較常用的 flexbox properties，它們不是全部，但學會這些，大概就能處理 90% 使用 flexbox 的場景了

其他例如 flexbox `order` property 我甚至認為應該避免使用，它會讓 DOM 順序的管理變得混亂，除非是非使用不可的場景，否則幾乎是沒有機會用到

就如同上面提到的，我覺得初學 flexbox 時若常常搞不清楚某個 property 的行為，則往往是因為忽略了 property 的**預設值**這件事情

文章的結尾附上一些常見的 flexbox properties 的所有可選值，與其預設值（粗體為預設值）

### flex container

- flex-direction: **row** | row-reverse | column | column-reverse
- flex-wrap: **nowrap** | wrap | wrap-reverse
- justify-content: **flex-start** | flex-end | center | space-between | space-around | space-evenly
- align-items: **stretch** | flex-start | flex-end | center | baseline
- align-content: **normal** | flex-start | flex-end | center | space-between | space-around | space-evenly | stretch
- flex-grow: **0**
- flex-shrink: **1**
- flex-basic: **auto**
- align-self: **auto** | flex-start | flex-end | center | baseline | stretch
