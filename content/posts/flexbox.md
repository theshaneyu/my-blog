---
title: 'Flexbox'
date: 2022-02-15T18:33:47+08:00
draft: false
---

本篇打算來記錄一下我學習 flexbox 的過程，算是以一個已經學會並且回頭看的角度，把一些後來的自己希望當初在學的時候能夠更加釐清的部分做一個紀錄

# 基本觀念

其中一個一開始沒弄明白但卻很重要的觀念就是：flexbox 相關的 properties 總共分成 **flexbox container properties** 和 **flexbox item properties** 兩種

所謂 flexbox container 也就是包覆著 flexbox items 的 parent elements

例如你想要針對一個 parent 下面三個 children 的排列方式進行設定，你可能會這樣安排你的 html

```html
<div class="flexbox-container">
  <div class="flexbox-item flexbox-item1"></div>
  <div class="flexbox-item flexbox-item2"></div>
  <div class="flexbox-item flexbox-item3"></div>
</div>
```

而 flexbox 的 properties 也就是分成專門給 **flexbox container**（設定在 `flexbox-container` class）與專門給 **flexbox items** （設定在 `flexbox-item1`、`flexbox-item2` 與 `flexbox-item3` classes）兩種 properties

其實 flexbox 的目的，也就是讓你能在不一個一個設定 flexbox item 的情況下彈性地調整 flexbox container 內 flexbox items **在一個方向上（水平或垂直）** 排列的方式

顯然這邊特別提到一個方向上，表示會有能夠在兩個方向上（水平和垂直）設定排列方式的屬性，也就是 `grid` property

# 預設值

承上方所描述的 html，今天將 flexbox item 相關 classes 做如下設定（省略掉一些無關的 styling）：

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

而如果我們希望這三個 items 按照 flexbox 的方式進行排列，只要在 `flexbox container` 內設定：

```css
.flexbox-container {
  display: flex;
}
```

便可將三個 items 像這樣做排列：

![original](/flexbox/first-flex.png)

這邊可以發現三件事情：

1. 三個 items 呈**水平方向**排列
2. 三個 items **靠左**排列
3. 三個不同高度的 items 變成**相同的高度**

這邊便會帶到另外一個後來的我希望當初學習 flexbox 時更加關注的事情：**flexbox properties 的預設值**

會出現上述三個現象是因為當我們把 flexbox container 的 `display` 設定為 `flex` 時，該 flexbox container 會自動擁有一些 flexbox properties，且它們將被設定為各自的**預設值**

1. `flex-direction` 被設定為預設值 `row`，使得三個 items 呈**水平方向**排列
2. `justify-content` 被設定為預設值 `flex-start`，使得三個 items **向左**靠攏
3. `align-items` 被設定為預設值 `stretch`，使得 item1 和 item2 被拉伸為**和 item3 相同的高度**

我也將在本篇的結尾附上一些我覺得比較重要的 properties 的預設值

接著再來複習一下，flexbox properties 分成用於設定 parent 的 flexbox container properties 和用於設定 children 的 flexbox item properties，接下來將會先介紹 flexbox container properties 再介紹 flexbox item properties

# flexbox container properties

## `justify-content` property

CSS styling 當中最常做的事情莫過於將一個 element **水平置中**，此時我們可以透過對 flexbox container 設定 `justify-content: center` 來達到水平置中

```css
.flexbox-container {
  display: flex;
  justify-content: center;
}
```

![justify-center](/flexbox/justify-center.png)

將 justify-content 設定為 `center` 後，所有 children items 將會被擠到中間，且彼此之間不會預留空間（此處的空隙是因為 `flexbox-item` class 有設定 margin）

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

如剛才所提到的，一但將 flexbox container 設定為 `display:flex`，三個 items 的高度都將會變成一樣，是因為 `align-items` 的預設值為 `stretch`，而如果將 `align-items` 設定為 `flex-start`，則三個 items 的高度將會回到原本的值，並且朝上靠攏

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

另一個不是很常用的 property 是 `align-content` property，align-content property 只會在**多行**的 flexbox items 中使用

如果我們將視窗的寬度縮窄，增加 flexbox container 的高度，並且將 flexbox container 的 `flex-wrap` 設定為 `wrap`，則 flexbox items 將呈 multi-line 排列

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

# flexbox item properties

flexbox item properties 用於設定某特定 flexbox item 的尺寸及排列方式等等

## `flex-shrink` property

預設情況下，如果我們將瀏覽器視窗的寬度縮小至小於 flexbox container 的寬度時，flexbox 會自動將每個 flexbox items 的寬度縮小

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

如果我們希望在 flexbox container 的寬度增加時，讓 item3 的寬度也隨之增加，並填滿所有剩餘的空間，可以設定 `flex-grow: 1`

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

align-self property 用於設定單一 flexbox item 於垂直方向對齊的方式

例如如果我們將 item2 設定 `align-self: center`，則 item2 將會回復到原本的高度（複習：item2 原本的高度是 200px，會被拉伸成 300px 是因為 flexbox container 的 align-items 值預設為 `stretch`），並且垂直置中

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

# Shorthand - `flex`

另一個常見用於設定 **flexbox item** 的方式是使用 shorthand - `flex` property

`flex` 為 `flex-grow`、`flex-shrink`、`flex-basis` 的縮寫

例如

```css
.flexbox-item {
  flex: 1 1 0px;
}
```

等同於

```css
.flexbox-item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basic: 0px;
}
```

然而和 `margin`、`padding` 等 properties 一樣，`flex` 可能不會有完整的三個數值

當 `flex` 只有**兩個**數值時，兩個數值可能分別代表：

1. `flex-grow` ＆ `flex-basis`
2. `flex-grow` ＆ `flex-shrink`

而當 `flex` 只有**一個**數值時，該數值可以是：

1. `flex-grow`
2. `flex-basis`
3. `none`
4. `inherit`

`flex` 的定義如果沒有記清楚，很容易會有預期外的效果，這邊提供幾個常見的用法

### `flex: 0 auto;`

這等同於 `flex: initial`，也等同於所有三個數值的預設值：`flex: 0 1 auto;`

這種寫法雖然沒有特別設定 `flex-shrink`，但其實已經預設把 `flex-shink` 設定為 `1`，因此該 flexbox item 會有它最初始預設的行為，也就是當 flexbox container 留有多餘的空間時，便可以根據 flexbox container 的設定來彈性地調整 flexbox items 的排列方式，同時在 flexbox container  被壓縮時，flexbox items 也跟著被壓縮。

### `flex: auto`

這等同於 `flex; 1 1 auto`，也就是 flexbox item 不但會空間不足時被壓縮，也會在有多餘空間時擴張。

### `flex: none`

這等同於 `flex: 0 0 auto`，也就是 flexbox items 不會被壓縮，也不會擴張，也就是完全不伸縮的意思。

### `flex: 1`

這等同於 `flex: 1 0px`，也等同於 `flex: 1 1 0px`，所以需要特別注意，**雖然沒有特別寫，但其實已經把 `flex-shrink` 設定為 `1`，也已經把 `flex-basix` 設定為 `0px` 了**，也就是 flexbox 會在假設該 item 寬度為 0 的情況下，將剩餘的空間依照該正整數的比例分配給該 flexbox item。

### `flex: 100px`

這等同於 `flex: 1 100px`，也等同於 `flex: 1 1 100px`，也就是，**雖然沒有特別寫，但其實已經把 `flex-shrink` 設定為 `1`，也已經把 `flex-grow` 設定為 `1` 了**

### `flex: 0 0`

等同於 `flex: 0 0 0px`，就是雖然看起來只有設定 `flex-grow` 和 `flex-shrink`，**但其實也把 `flex-basic` 設定成 `0` 了**

由以上例子可以歸納出：

- 除了 `none` 之外，只要沒有特別設定，`flex-shrink` 都會被預設為 `1`，也就是預設該 flexbox item 無論如何都會在空間不足時被壓縮

- 當數值只有一個值，且該數值如果是 **pixel 值**，則代表 `flex-grow` 被預設為 `1`，也就是**當 `flex` 被設定為像素質的時候，代表你希望設定該 flexbox item 會擴張，且會以 `flex-basic` 為該像素質的基礎進行擴張**

- 當數值只有一個值，且該數值是**正整數**，則代表 `flex-basic` 被預設為 `0px`，也就是**當 `flex` 被設定為正整數的時候，代表你希望設定該 flexbox item 在 `flex-basic` 為 `0px` 的基礎上，進行擴張，且以該正整數的比例進行擴張**

# Flexbox properties values

文章的結尾附上一些常見的 flexbox properties 的所有可選值，與其預設值（粗體為預設值）

### flexbox container

- flex-direction: **row** | row-reverse | column | column-reverse
- flex-wrap: **nowrap** | wrap | wrap-reverse
- justify-content: **flex-start** | flex-end | center | space-between | space-around | space-evenly
- align-items: **stretch** | flex-start | flex-end | center | baseline
- align-content: **normal** | flex-start | flex-end | center | space-between | space-around | space-evenly | stretch
- flex-grow: **0**
- flex-shrink: **1**
- flex-basic: **auto**
- align-self: **auto** | flex-start | flex-end | center | baseline | stretch
