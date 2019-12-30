
# CSS選擇器



`.one.two`：只有同時擁有.one.tw的會被選到，例如`<div class="one two box">`
`.one, .two`：只要有one 或是 two就會被選到
`.one .two`：one下面所有的two都會被選到
`.header > img {}`：class為header下第一層碰到的元素為img，此img才會被選到


`overflow: hidden`  超出此層框架的內文會被隱藏(hidden)
`line-clamp: 2` 依照指定行數，使得行數後的內文以刪節號代替。