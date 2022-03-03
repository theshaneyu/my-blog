---
title: 'Flexbox'
date: 2022-02-15T18:33:47+08:00
draft: false
---

## 基本觀念

當我回頭看當初學習 flexbox 時，比較沒有釐清但是卻是最重要的觀念就是：**flexbox 相關的 properties 總共分成 `flex container` 與 `flex items` 兩種**。

所謂 flex container 也就是包含著 flex items 的 parent elements。例如你想要針對三個 child items 在一個 parent element 中排列的方式進行設定，你可能會這樣安排你的 html：

```html
<div class="flexbox-container">
  <div class="flexbox-item flexbox-item1"></div>
  <div class="flexbox-item flexbox-item2"></div>
  <div class="flexbox-item flexbox-item3"></div>
</div>
```

而 flexbox 的 properties 也就是分成專門給 `flex container` 的屬性（設定在 `flexbox-container` class）與專門給 `flex items` 的屬性（設定在 `flexbox-item1`、`flexbox-item2` 等等 classes）

其實 Flexbox 的目的，也就是讓你能在不各自設定不同 flex item 的情況下，能夠彈性地調整 flex container 內 flex items 們排列的方式。

<br />

## `justify-content` 與 `align-items` properties

其實理解了 `justify-content` 與 `align-items` 的定義，大概也就學會了 flexbox 80% 的用法了，這兩個 properties 是最常用的屬性。

承上方所描述的 html，今天將 `.flex-container` 與 `.flex-items` 做如下設定：

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

會得到這樣的三個矩形：

![original](/flexbox/original.png)
