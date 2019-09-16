
### get Proprty from Object 獲得物件屬性的方法

#### Proprty 屬性

1. self property 自有屬性
  -  IsEnumerable 可枚舉: Object.keys(obj), for ... in 
  -  not Nnumerable 不可枚舉



2. prototype from prototype 
  - IsEnumerable 可枚舉: for ... in 
  - not Nnumerable 不可枚舉

* getOwnPropertyNames: get all property from object 
  

#### Conclusion

- Object.keys(obj)：get all `self`'isenumerable property(可以把自有且可枚舉的屬性組成陣列)
- for .. in ：get all isenumerable property (可以把`自有`、`繼承`且可枚舉的屬性組成陣列)
- getOwnPropertyNames：get all property (可以把`自有`、`繼承`的`所有`屬性組成陣列)