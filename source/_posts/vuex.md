---
title: First to tager blog
date: 2018-05-13 22:30:36
categories: ['vue']
tags: ['vuex']
---
Hello world，vuex！！
vue+vuex : https://www.tuicool.com/articles/vQBbiiQ
...mapGetters和...mapState获取到的state，怎么拿来在methods中操作？https://segmentfault.com/q/1010000009566654
Vuex中mapState的用法https://www.cnblogs.com/meiyh/p/6805987.html

https://blog.csdn.net/youzhiningo/article/details/79640388

vuex 
state: 通过commit触发mutations的方法来设置state,通过计算属性跟踪获取store.state.xx.
module中的state，用store.state.moduleName.xx获取。
Excute order--->> methods里with commit set state---触发store中的mutions---computed里获取state
注意state.moduleName根据模块名获取。

getter : Getters 我们可以理解为store仓库的一个计算属性，它的作用主要是用来派生出一些新的状态。比如我们要把state状态的数据进行一次映射或者筛选，再把这个结果重新计算并提供给组件使用。
此时，getters 会暴露出一个store.getters对象，我们就可以在任何组件中使用this.$store.getters.xxx来绑定数据。
作用：1. 一般用于过滤数据，
     2.减少代码量，把各组件中的计算属性的状态逻辑抽离到getters中。
Excute order--->> methods里with commit set state---触发store中的mutions---computed里获取this.$store.getters.xxx来绑定数据自动触发store中的getters方法并将返回的值映射到computed。

mutations:更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。 必须是同步提交。
注意： module内外的getters不能duplicate,  mutation可以有duplicate。

action:Action 提交的是 mutation，而不是直接变更状态。
Action 可以包含任意异步操作。

module


辅助函数的目的都是为了缩写，提高效率。
mapState辅助函数(写在computed中)：
有多个state时，辅助函数帮助我们生成计算属性，让你少按几次键：
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
当映射的计算属性的名称与 state 的子节点名称相同时，我们也可以给 mapState 传一个字符串数组。
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
注意映射module中的state不能用数组，必须用对象，因为获取module中的state要加moduleName.

mapGetters （写在computed中）
辅助函数仅仅是将 store 中的 getter 映射到局部计算属性，store.getters.xx不需要moduleName。

mapMutations（写在methods中）
映射代替this.$store.commit（xxx）

mapActions （也是写在methods中）
用法同mapMutations

应该只有store在module中是独立的。
mutations和getters触发都是先触发外层的再触发module内的mutaions和getters对应的方法。module内的mutations和getters在computed中调用时是不需要加module名的。
不能有duplicate getter key， 可以有duplicate mutation key, 用commit可以触发所有duplicate mutation key, 由外向内的module mutation触发。

ES2017 新特性：Async Functions (异步函数)http://www.css88.com/archives/7731
http://www.jb51.net/article/96100.htm
https://segmentfault.com/a/1190000008011822
http://www.css88.com/archives/7980
await到底在等啥？https://segmentfault.com/a/1190000007535316
async函数的再次了解？？？
有时间再深入理解异步编程：阮一峰： http://www.ruanyifeng.com/blog/2015/05/async.html
vue-router  scrollBehavior ？
