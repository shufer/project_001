<template>
  <div class="todoapp">
    <TodoHeader @create="createFn"></TodoHeader>
    <TodoMain :arr="showArr" @del="deleteFn"></TodoMain>
    <TodoFooter @changeType="typeFn" :farr="showArr" @clear="clearF"></TodoFooter>
  </div>
</template>

<script>
// import styles
import "./styles/base.css"
import "./styles/index.css"

//import components
import TodoHeader from './components/TodoHeader.vue';
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";

export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list:[
        { id: 100, name: "吃饭", isDone: true },
        { id: 201, name: "睡觉", isDone: false },
        { id: 103, name: "打豆豆", isDone: true },
      ],
      getSel:"all"
      }
  },
  methods: {
    createFn(taskName) {
      let id = this.list.length == 0 ? 100 : this.list[this.list.length - 1].id + 1
      this.list.push({
        id:id,
        name:taskName,
        isDone:false
      })
    },
    deleteFn(theId) {
      let index = this.list.findIndex(obj => obj.id === theId)
      this.list.splice(index,1)
    },
    typeFn(str) {
      this.getSel = str
    },
    clearF() {
      this.list=this.list.filter(obj => obj.isDone == false)
    }
  },
  computed: {
    showArr(){
      if (this.getSel === 'yes') {
        return this.list.filter(obj => obj.isDone === true);
      } else if (this.getSel === 'no') {
        return this.list.filter(obj => obj.isDone === false);
      }else {
        return this.list;
      }
    }
  }
}
</script>

<style>

</style>
