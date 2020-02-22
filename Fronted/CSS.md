
# CSS選擇器

- `.one.two`：只有同時擁有.one.tw的會被選到，例如`<div class="one two box">`
- `.one, .two`：只要有one 或是 two就會被選到
- `.one .two`：one下面所有的two都會被選到
- `.one > img`：class為header下第一層碰到的元素為img，此img才會被選到

## CSS

- `:not()`:不是
- `:last-child`:身為最後一個元素
- `:after`:在元素後面加東西

```css
    :not(:last-child):after {    
        /* 非最後一個child的元素後面加上'|'  */
        content:"|";
    }
```

# SCSS

- `.one { &.two {} }`:等同於`.one.two`
- `.one { .two {} }`:等同於`.one .two`
- `.one { > two {} }`:等同於`.one > two`

```css
.one {
    &.two{
       background:blue;
    }
}

/* compiles to: */
.one.two {
    background: blue;
}
```


```css
.one {
    .two{
       background:blue;
    }
}

/* compiles to: */
.one .two {
    background: blue;
}
```

# 有趣的屬性

- `overflow: hidden`  超出此層框架的內文會被隱藏(hidden)
- `line-clamp: 2` 依照指定行數，使得行數後的內文以刪節號代替。

# 排版

## Flex排版

###  display: flex 可以讓裡面的item並排

```css
.flex-container {
  display: flex;
}
```

### flex-direction 可以決定裡面item的排列方向

```css
.flex-container {
  display: flex;
  flex-direction: row;  /* 水平排列 */
}
```

flex-direction: row;  /* 水平排列 */
flex-direction: column;  /* 垂直排列 */
flex-direction: row-reverse;
flex-direction: column-reverse;

### flex-wrap

不希望 flex items 溢出 container 時，你可以使用 flex-wrap 來「包裝」內容，也就是讓他們遇到邊界就「自動換行」，不然裡面的item就愈來愈小（壅擠）

```css
.flex-container {
  display: flex;
  flex-direction: row;  /* 水平排列 */
  flex-wrap:wrap;
}
```

flex-wrap: no-wrap
flex-wrap: wrap
flex-wrap: wrap-reverse

### flex-flow

flex-direction 和 flex-wrap 這兩個屬性可以合併成 flex-flow 屬性。flex-flow 接受兩個值，第一個是給 flex-direction 第二個是給 flex-wrap。例如：


```css
.flex-container {
    flex-flow: row wrap;
}
```

### justify-content  讓元素水平（X軸）置中

justify-content 可用的值

- flex-start (default)
- flex-end
- center

- space-between
- space-around
- space-evenly

### align-items  讓元素垂直（Ｙ軸）置中

- flex-start - item 會貼齊交叉軸的起點
- flex-end - item 會貼齊交叉軸的終點
- center - item 會對齊交叉軸的中間
- baseline - 先把內容對齊 baseline，item 隨著跑 (通常文字下緣對齊的地方稱為 baseline）
- stretch - item 會延展填滿容器空間，但會尊重特別指定的 width or height (如方塊 3)

### 垂直置中

```css
body {
  height: 500px;
  display: flex;  /* 讓裡面的元素併排 */
  justify-content: center; /* 讓元素置中 */
  align-items: flex-start; /* 讓垂直置中 */
}
```