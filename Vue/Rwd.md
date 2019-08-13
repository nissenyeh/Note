### Vue RWD (Vue上面的RWD技巧)

#### With Grid

- bootstrap-grid css
```html
<div class="container">
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-6">
      2 of 3 (wider)
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-5">
      2 of 3 (wider)
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
</div>
```
- elment-UI grid

```html
  <el-col :span="18">
  </el-col>
```

### When Grid is useless (不能用 Grid 的時候)

- 例如大小在tag自己的屬性上

#### Dont watch screen Width (不用監測螢幕寬度時)

``` html
<el-dialog
  width="90%" // Hope number smaller when in smaller screen
  center>
</el-dialog>
```

- 利用 `Regular Expression` + `window.innerWidth`

``` html
<el-dialog
  :width="isMobile ? '90%' : '30%'"
  center>
</el-dialog>

export default class HelperButton extends Vue {
 isMobile: boolean = window.innerWidth < 768;
}
```

#### Watch screen Width (要監測螢幕寬度變化時)



```js
  @Watch('winWidth')
  resize() {
    .... = this.winWidth < 460;
  }

  handleResize() {
    this.winWidth = window.innerWidth;
  }

  created() {
    window.addEventListener('resize', his.handleResize);
  }
```