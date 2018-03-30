---
title: Flexbox-totally-understanding
date: 2017-12-15 12:11:46
tags: [css, flexbox]
category: css
---

# Flexbox Totally Understanding

一直以來對 Flexbox 如何計算其 flex-grow, flex-basis, flex-shrink 有很大的疑惑，
今天有時間來好好研究一番，這篇 [css-trick 文章](https://css-tricks.com/flex-grow-is-weird/)一邊實作，並一邊核對與自己所理解的 flexbox 行為是否一致，
一步步帶我理解運作原理，廢話不多說，進入主題：

**flex-grow 是基於所剩寬度(parent寬度 - children總寬度)按比例分配給各children**
**將各子元素原始寬度+各剩餘寬度分配下來的數值，就是最終子元素寬度結果**

```// pug
.main
  .section Some Txt here...
  .aside So many texts here here and here, more than section's content text!
```

```// css
.main
  display: flex
  width: 900px

.section
  flex-grow: 2

.aside
  flex-grow: 1
```

> [情況一](https://codepen.io/matuzo/pen/ZQEWjg): 假設子元素有文字，子元素實際寬度則自動為文字內容最長寬度
> parent width: 900px
> section width: 99px
> aside width: 623px
> total flex-grow values: 3 -> 子元素 flex-grow 加總值

> **算出剩餘寬度**
> 剩餘寬度: 900 - 99 - 623 = 178px
>
> section flex-grow 為 2
> aside flex-grow 為 1

> **將剩餘寬度分配給子元素**
> section width: 178 x 2/3 = 118px
> aside width: 178 x 1/3 = 60px

> **各子元素原本寬度加上分配寬度 才是最後各子元素真實寬度**
> section width: 99px + 118px = <b style="color: #369">217px</b>
> aside width: 623px + 60px = <b style="color: #369">683px</b>



```// pug
.main
  .section
  .aside
```

```// css
.main
  display: flex
  max-width: 900px

.section
  flex-grow: 2
  flex-basis: 400px

.aside
  flex-grow: 1
  flex-basis: 200px
```
> [情況二](https://codepen.io/matuzo/pen/ZQEWjg): 假設子元素'沒有'文字，但 flex-basis 自訂子元素寬度
>
> parent width: 900px
> section width: 400px (flex-basis value)
> aside width: 200px (flex-basis value)
> total flex-grow values: 3 -> 子元素 flex-grow 加總值

> **算出剩餘寬度**
> 剩餘寬度: 900 - 400 - 200 = 300px
>
> section flex-grow 為 2
> aside flex-grow 為 1
>
> **將剩餘寬度分配給子元素**
> section width: 300 x 2/3 = 200px
> aside width: 300 x 1/3 = 100px
>
> **各子元素原本寬度加上分配寬度 才是最後各子元素真實寬度**
> section width: 400px + 200px = <b style="color: #369">600px</b>
> aside width: 200px + 100px = <b style="color: #369">300px</b>



```// css
.main
  display: flex
  max-width: 900px

.section, .aside
  padding: 20px
  margin: 15px

.section
  flex-grow: 2
  flex-basis: 200px

.aside
  flex-grow: 1
  flex-basis: 150px
```
> [情況三](https://codepen.io/matuzo/pen/wMaeVO): 如果子元素有 margin, padding，記得在一開始計算剩餘寬度時就要減掉

> **算出剩餘寬度(沒有 border-box 時只需減掉 margin )**
> 剩餘寬度: 900 - 200 - 150 - (15x4) = 490px
>
> **將剩餘寬度分配給子元素**
> section width: 490 x 2/3 = 326.666px
> aside width: 490 x 1/3 = 163.333px
>
> **各子元素原本寬度加上分配寬度 才是最後各子元素真實寬度**
> section width: 200px + 326px = <b style="color: #369">526px</b>
> aside width: 150px + 163px = <b style="color: #369">313px</b>