# 借鉴vue实现的观察者
参考了vue的源码：https://github.com/vuejs/vue
### 使用
```Javascript
import Vue from './Vue';
import Watcher from './Watcher';

function bindCallback(newValue, oldValue) {
    console.log('bindCallback', newValue, oldeValue);
}

// 观察的数据
let data = {
    test: "123";
}

// 观察
let vm = new Vue(data);

// 订阅data.test的变化，当data.test的值变化的时候触发 bindCallback;
let watcher = Vue.bind(new Watcher(vm, bindCallback, this), data.test);
// or let watcher = Vue.bind(new Watcher(vm, bindCallback, this), vm.test)

// 修改data.test的值，触发bindCallback
vm.test = "456";

// 取消订阅，data.test值再变化的时候不再触发回调
watcher.teardown()
// 修改data.test的值，但不再触发回调
vm.test = "789";
```