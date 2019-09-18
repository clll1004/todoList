<template>
  <div id="app">
    <t-header></t-header>
    <t-input v-on:passItem="addItem"></t-input>
    <t-list v-bind:props="todoLists" v-on:passRemove="removeItem" v-on:passStatus="toggleStatus"></t-list>
  </div>
</template>
<script>
import THeader from './comp/THeader.vue';
import TInput from './comp/TInput.vue';
import TList from './comp/TList.vue';

export default {
  name: 'app',
  components: {
    THeader,
    TInput,
    TList
  },
  data() {
    return {
      todoLists: [],
      listIndex: 0
    }
  },
  created() {
    let imp_list = [];
    let normal_list = [];
    for (let i = 0; i < localStorage.length; i++) {
      if (localStorage.getItem(localStorage.key(i)) !== 'SILENT') {
        const tmp = JSON.parse(localStorage.getItem(localStorage.key(i)));
        tmp.important ? imp_list.push(tmp) : normal_list.push(tmp);
      }      
    }
    this.todoLists = imp_list.sort(this.sortLists).concat(normal_list.sort(this.sortLists));
    this.listIndex = this.todoLists.length;
  },
  methods: {
    sortLists(a, b) {
      if ( a.idx < b.idx ){
        return -1;
      }
      if ( a.idx > b.idx ){
        return 1;
      }
      return false;
    },
    addItem(item) {
      let tmp = {title: item, complete: false, important: false, idx: this.listIndex}
      this.todoLists.forEach(comp => {
        if (comp.title === item) {
          tmp = false;
        }
      });
      if (tmp) {
        this.todoLists.push(tmp);
        localStorage.setItem(tmp.title, JSON.stringify(tmp));
        this.listIndex += 1;
      } else {
        alert('이미 등록되어있는 투두입니다.');
      }
    },
    removeItem(idx) {
      localStorage.removeItem(this.todoLists[idx].title);
      this.todoLists.splice(idx, 1);
    },
    toggleStatus(idx, action) {
      const tmp = this.todoLists[idx];
      tmp[action] = !tmp[action];
      if (action === 'important') {
        this.setSortList(idx);
      }
      localStorage.setItem(tmp.title, JSON.stringify(tmp));
    },
    setSortList(idx) {
      const tmp = this.todoLists[idx];
      this.removeItem(idx);
      this.todoLists.unshift(tmp);
    }
  }
}
</script>
<style>
  * {
    margin: 0;
    padding: 0;
    font-size: 14px;
  }
  body {
    width: 100%;
    min-height: calc(100vh - 60px);
    background: linear-gradient(45deg, #a6d7de, #fa9c9c) no-repeat;
    box-sizing: border-box;
  }
  #app {
    width: 95%;
    min-width: 300px;
    max-width: 500px;
    min-height: 535px;
    padding: 30px;
    margin: 30px auto;
    background: rgba(255, 255, 255, .93);
    border-radius: 3px;
    box-sizing: border-box;
  }  
</style>
