

``` js
  <FormRow>

    <template slot="left"> //放到left插槽
      <FormLabel for="last-name">身分證上的姓氏*</FormLabel>  
      <ToolTip text="請填寫與身分證件相符之姓名以利核對"/>
    </template>
    
    <TextInput
      id="last-name"
      slot="right"
      placeholder="熊"
      :value.sync="lastName"
      :disabled="submitted">
    </TextInput>
  </FormRow>
```

```js
<div :class="$style.formRow">

  <div v-if="slots().left" :class="$style.left">
    <slot name="left"/> 
  </div>

  <div v-if="slots().right" :class="$style.right">
    <slot name="right"/> 
  </div>

  <div :class="$style.full">
    <slot/>
  </div>

</div>
```