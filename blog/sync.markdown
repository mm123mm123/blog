# .sync修饰符
```
//App.vue
<template>
  <div class="app">
    App.vue 我现在有 {{total}}
    <hr>
    <Child :money="total" v-on:update:money="total = $event"/>
  </div>
</template>

<script>
import Child from "./Child.vue";
export default {
  data() {
    return { total: 10000 };
  },
  components: { Child: Child }
};
</script>

<style>
.app {
  border: 3px solid red;
  padding: 10px;
}
</style>


//Child.vue
<template>
  <div class="child">
    {{money}}
    <button @click="$emit('update:money', money-100)">
      <span>花钱</span>
    </button>
  </div>
</template>

<script>
export default {
  props: ["money"]
};
</script>


<style>
.child {
  border: 3px solid green;
}
</style>
```
在子组件的内部去修改money会报错，所以我们通过eventBus原理来修改这个值当点击button时，会执行$emit，
它会触发update:money事件，并且把money-100传给$event变量。之后父组件加在update:money上的监听器监听到了触发，
会执行这个事件，就是把$event传给了total，而又因为money=total,所以最终更新之后的值又回到了子组件
```
<tmplate>
    <div class="app">
        App.vue我现在月{{tatal}}
        <hr>
        <Child :money.sync="tatal"/>
</template>
```
而vue发明了.sync这个修饰符，就是用来处理上面的这种情况，从图中可以看到，在属性后面加上此修饰符，
就可以替代v-on:update:money="total = $event 这串代码
所以.sync代表的动作就是给子组件指定属性添加监听器，用来监听它的更新，并且将更新动作传给父组件里面的对应属性
