<template>
  <div id="app">
   <!-- 接受传过来的题目 -->
    <h1>{{title}}</h1>
    <input id="add-input" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
        <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
          {{item.label}}
        </li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'
export default {
  //数据
   data () {
      return {
        //写一个标题传过去
        title: 'This is a todo list',
        //传过去的一个数组
        items: Store.fetch(),
        newItem: ''
      }
    },
    watch: {
      items: {
        handler: function(items) {
            Store.save(items)
        },
        deep: true
        }
    },
   // 方法
   methods: {
          toggleFinish: function (item){
                item.isFinished = !item.isFinished
          },
          addNew: function (){
            if(this.newItem!=''&&this.newItem!=null){
                this.items.push({
                  label : this.newItem,
                  isFinished: false
                }) 
                 this.newItem = '' 
              }
          }
        }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
#app {
  width: 800px;
  margin: 30px auto;

}

ul{
  
  padding: 0 2%;
}
#add-input {
  width: 750px;
  height: 35px;
  padding: 0 5px;
}


.finished{
  text-decoration: underline;
}


</style>
