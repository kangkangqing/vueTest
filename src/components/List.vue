<template>
<ul style="padding: 0;">
  <Item v-for="item in todos" :key="item.id" :todo="item"
  ></Item>
</ul>
</template>

<script>
import Item from '../components/Item'
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "List",
  components:{
    Item
  },
  data(){
    return{
    }
  },
  props:['todos']
}
</script>

<style scoped>

</style>