<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input @passItem="addItem"></todo-input>
    <ul class="list_area" v-if="todoLists.length !== 0">
      <li v-for="(todoItem, index) in todoLists" :key="todoItem.key" :class="todoItem.complete ? 'done' : ''">
        <em @click="toggleComplete(index)"><i class="fa fa-check"></i></em>
        <strong @click="toggleComplete(index)">{{todoItem.title}}</strong>
        <p v-if="todoItem.time !== 'x' || todoItem.place" >
          <span v-if="todoItem.time !== 'x'">{{todoItem.time}}:00 &nbsp;</span><span v-if="todoItem.place">{{todoItem.place}}</span>
        </p>
        <span class="btn_imp" :class="todoItem.important ? 'on' : ''" @click="toggleImportant(index)"><i class="fa fa-star"></i></span>
        <span class="btn_remove" @click="removeItem(index)"><i class="fa fa-times"></i></span>
      </li>
    </ul>
    <no-data v-if="todoLists.length === 0"></no-data>
    <todo-footer :propsTotalCount="todoLists.length" :propsCompleteCount="completeCount" @passClear="clearAllTodo" @passDoneAll="doneAllTodo"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import NoData from './components/NoData.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  name: 'app',
  components: {
    TodoHeader,
    TodoInput,
    NoData,
    TodoFooter
  },
  data() {
    return {
      todoLists: [],
      viewLists: [],
      listIdx: 0,
      completeCount: 0
    }
  },
  created() {
    for (let i = 0; i < localStorage.length; i++) {
      if (localStorage.getItem(localStorage.key(i)) !== 'SILENT') {
        const tmp = JSON.parse(localStorage.getItem(localStorage.key(i)));
        this.todoLists.push(tmp);
        this.listIdx += 1;
      }      
    }
    this.init();
  },
  methods: {
    init() {
      this.setCompleteCount();
      this.viewLists = this.todoLists.sort(this.sortLists);
      console.log(this.viewLists);
    },
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
      const tmp = { idx: this.listIdx, complete: false, title: item.title, time: item.time, place: item.place, important: false };
      this.todoLists.push(tmp);
      localStorage.setItem(tmp.idx, JSON.stringify(tmp));
      this.listIdx += 1;
    },
    toggleComplete(idx) {
      this.todoLists[idx].complete = !this.todoLists[idx].complete;
      localStorage.setItem(this.todoLists[idx].idx, JSON.stringify(this.todoLists[idx]));
      this.setCompleteCount();
    },
    toggleImportant(idx) {
      this.todoLists[idx].important = !this.todoLists[idx].important;
      localStorage.setItem(this.todoLists[idx].idx, JSON.stringify(this.todoLists[idx]));
    },
    removeItem(idx) {
      localStorage.removeItem(this.todoLists[idx].idx);
      this.todoLists.splice(idx, 1);
      this.setCompleteCount();
    },
    doneAllTodo() {
      if (confirm('모든 일감을 완료하셨나요?')) {
        for (let i = 0; i < this.todoLists.length; i++) {
            this.todoLists[i].complete = true;
            localStorage.setItem(this.todoLists[i].idx, JSON.stringify(this.todoLists[i]));
        }
        this.completeCount = this.todoLists.length;
      }
    },
    clearAllTodo() {
      if (confirm('모든 일감을 삭제할까요?')) {
        localStorage.clear();
        this.todoLists = [];
        this.completeCount = this.todoLists.length;
      }
    },
    setCompleteCount() {
      this.completeCount = 0;
      for (let i = 0; i < this.todoLists.length; i++) {
        if (this.todoLists[i].complete) {
          this.completeCount += 1;
        }
      }
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
.list_area {
  min-height: 300px;
}
.list_area li {
  position: relative;
  padding: 10px 40px 15px;
  margin-bottom: 15px;
  list-style: none;
  border: 1px solid #e9e9e9;
  border-left: 1px solid #a6d7de;
  box-sizing: border-box;
  word-break: break-all;
}
.list_area li:hover {
  background: rgba(167,215,222,.07);
  border-left: 2px solid #a6d7de;
}
.list_area li strong {
  cursor: pointer;
}
.list_area li em {
  position: absolute;
  left: 5px; top: 0;
  width: 30px;
  height: 100%;
  text-align: center;
  cursor: pointer;
}
.list_area li em i {
  position: absolute;
  top: calc(50% - 10.5px); left: 2px;
  width: 13px; height: 13px;
  padding: 2px;
  line-height: 13px;
  background: #fff;
  color: #ddd;
  border: 2px solid #ddd;
  border-radius: 50px;
}
.list_area li.done {
  background: rgba(0,0,0,.04);
}
.list_area li.done:hover {
  border-left: 1px solid #a6d7de;
}
.list_area li.done strong {
  color: #888;
  text-decoration-line: line-through;
}
.list_area li.done em i {
  color: #a6d7de;
  border:2px solid #a6d7de;
}
.list_area li p {
  color: #999;
  font-size: 13px;
  margin-top: 5px;
}
.btn_imp {
  position: absolute;
  top: calc(43% - 7px); right: 32px;
  width: 11px; height: 14px;
  color: rgba(0,0,0,.3);
  cursor: pointer;
}
.btn_imp.on, .btn_imp.on:hover, .btn_imp.on:active {
  color: #ffc516;
}
.btn_remove {
  position: absolute;
  top: calc(41% - 7px); right: 15px;
  width: 11px; height: 14px;
  color: rgba(0,0,0,.3);
  cursor: pointer;
}
.btn_imp:hover, .btn_imp:active, .btn_remove:hover, .list_area li .btn_remove:active {
  color: rgba(0,0,0,.5);
}
</style>
