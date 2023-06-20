<template>

    <li style="list-style: none;display: flex;justify-content: space-between">
      <label>
<!--        <input type="checkbox" v-model="todo.done">-->
<!--        不让修改props，因为修改的是对象的属性值，vue检测不到，所以不会报错-->
        <input type="checkbox" :checked="todo.done" @change="changeCheck(todo.id)" v-show="!todo.isEdit">
        <span v-text="todo.name" v-show="!todo.isEdit"></span>
        <input type="text" :value="todo.name" v-show="todo.isEdit" @blur="save(todo,$event)"
        ref="input"
        >
      </label>
      <div style="display: flex;flex-direction: row">
        <button @click="editTodo(todo)" v-show="!todo.isEdit">编辑</button>
        <button @click="deleteTododo(todo.id)">删除</button>
      </div>

    </li>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Item",
  props:['todo'],
  methods:{
    //将id参数传回父组件
    changeCheck(id){
      // console.log(id)
      this.$bus.$emit('updateCheck',id)
    },
    deleteTododo(id){
      if(confirm("确定删除吗"))
      this.$bus.$emit('deleteTodo',id)
    },
    //编辑todo
    editTodo(todo){
      // 首次添加属性后，之后不必再添加属性了
      if(Object.prototype.hasOwnProperty.call(todo,'isEdit')){
        todo.isEdit=true
      }else {
        this.$set(todo,'isEdit',true)
      }
      //修改了属性后，vue并没里马解析模板，出现input，所以input获取焦点不生效
      //将获取焦点放在下一轮更新即可
      this.$nextTick(function (){
        //获取焦点
        this.$refs.input.focus()
      })
      //使用定时器也是可以解决的

    },


    //失去焦点
    save(todo,event){
      todo.isEdit=false
      //这样也行，但是修改了props值了
      // todo.name=event.target.value
      //使用全局事件总线后
      this.$bus.$emit('updateTodo',todo.id,event.target.value)

    }

  }
}
</script>

<style scoped>
button{
  display: none;
}
li:hover{
  background: aquamarine;
}
li:hover button{
  display: block;
}
</style>