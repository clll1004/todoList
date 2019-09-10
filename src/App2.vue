<template>
  <div id="app">
    <THeader></THeader>
    <TInput v-on:passItem="addItem"></TInput>
    <ul class="list_area">
      <li v-for="(list, index) in todoLists" :key="list.key" :class="list.complete ? 'done' : ''">
        <em @click="toggleStatus(index, 'complete')"><i class="fa fa-check"></i></em> 
        <span class="title" @click="toggleStatus(index, 'complete')">{{list.title}}</span>
        <span class="btn_imp" :class="list.important ? 'on' : ''" @click="toggleStatus(index, 'important')"><i class="fa fa-star"></i></span>
        <span class="btn_remove" @click="removeItem(index)"><i class="fa fa-times"></i></span>
      </li>
    </ul>
  </div>
</template>
<script>
import THeader from './comp/THeader.vue';
import TInput from './comp/TInput.vue';
export default {
  name: 'app',
  components: {
    THeader,
    TInput
  },
  data() {
    return {
      todoLists: []
    }
  },
  methods: {
    addItem(item) {
      let tmp = {title: item, complete: false, important: false}
      this.todoLists.forEach(comp => {
        if (comp.title === item) {
          tmp = false;
        }
      });
      if (tmp) {
        this.todoLists.push(tmp);
        localStorage.setItem(tmp.title, JSON.stringify(tmp));
      } else {
        alert('이미 등록되어있는 투두입니다.');
      }
    },
    removeItem(idx) {
      this.todoLists.splice(idx, 1);
    },
    toggleStatus(idx, action) {
      this.todoLists[idx][action] = !this.todoLists[idx][action];
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
  .list_area {
    min-height: 300px;
    margin-top: 20px;
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
  .list_area li span {
    cursor: pointer;
  }
  .list_area li .title {
    display: inline-block;
    padding-right: 10px;
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
    top: calc(50% - 10.5px); left: 4px;
    width: 13px; height: 13px;
    padding: 2px;
    line-height: 13px;
    background: #fff;
    color: #ddd;
    border: 2px solid #ddd;
    border-radius: 50px;
  }
  .list_area li.done em i {
    color: #a6d7de;
    border:2px solid #a6d7de;
  }
  .list_area li.done .title {
    text-decoration: line-through; 
  }
  .btn_imp {
    position: absolute;
    top: calc(43% - 7px); right: 32px;
    width: 11px; height: 14px;
    color: rgba(0,0,0,.3);
  }
  .btn_imp.on, .btn_imp.on:hover, .btn_imp.on:active {
    color: #ffc516;
  }
  .btn_remove {
    position: absolute;
    top: calc(41% - 7px); right: 15px;
    width: 11px; height: 14px;
    color: rgba(0,0,0,.3);
  }
  .btn_imp:hover, .btn_imp:active, .btn_remove:hover, .list_area li .btn_remove:active {
    color: rgba(0,0,0,.5);
  }
</style>
