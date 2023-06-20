<template>
  <div>
    <input placeholder="请输入你的任务名称，回车键确认"
           v-model="renwu" @keyup.enter="submit"
           style="width: 40%"
    >
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: "MyHeader",
  data() {
    return {
      renwu: ""
    }
  }
,
  methods: {
    submit() {
      if (!this.renwu) {
        return
      }
      const  todo={
        id:nanoid(),
        name:this.renwu,
        done:false
      }
      this.$emit("getData",todo)
      this.renwu=''
    }
  }
}
</script>

<style scoped>

</style>