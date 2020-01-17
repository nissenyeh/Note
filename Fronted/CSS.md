
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

- flex置中排版

```css
body {
  height: 500px;
  display: flex;  /* 讓裡面的元素併排 */
  justify-content: center; /* 讓元素置中 */
  align-items: flex-start;
}
```