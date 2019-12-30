
# CSS選擇器


`.one .two{}`：one裡面的two才會被選到
`.one.two{}`：只有同時擁有.one.tw的會被選到，例如`<div class="one two box">`
`.one, .two{}`：只要有one 或是 two就會被選到
`.header > img {}`：class為header下第一層碰到的元素為img，此img才會被選到