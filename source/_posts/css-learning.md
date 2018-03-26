---
title: CSS-learning
date: 2017-06-09 17:05:50
tags: css
category: css
---

# Self Learning Note

1\. 在命名 css 時需先以是否為元件進行思考，如是元件，可依 BEM 命名規則: 元件/子元件/修飾符

```
.menu               // component
.menu--bgBlack      // modifier  --
.menu-list          // child-component  -
.menu-list--large   // child-component modifier --
{...}
```

2\. 如要重複使用元件，例如 card 這類元件，但又因不同頁面要微調樣式，可以在頁面/父元素掛 class 再以階層方式調整，但必須放在 _card.sass 方便統一管理

```
// default component css style
// at page A
.card
.card-item


// use card in different page
// at page B
.pageB
  .card
  .card-item


// same page different block
  // promote
  .promote
    .card
    .card-item

  // price
  .price
    .card
    .card-item
```


