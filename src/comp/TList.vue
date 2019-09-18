<template>
    <div>
        <div class="nodata" v-if="!props.length">
            리스트가 없습니다.
        </div>
        <ul class="list_area">
        <li v-for="(list, index) in props" :key="list.key" :class="list.complete ? 'done' : ''">
            <em @click="passStatus(index, 'complete')"><i class="fa fa-check"></i></em> 
            <span class="title" @click="passStatus(index, 'complete')">{{list.title}}</span>
            <span class="btn_imp" :class="list.important ? 'on' : ''" @click="passStatus(index, 'important')"><i class="fa fa-star"></i></span>
            <span class="btn_remove" @click="passRemove(index)"><i class="fa fa-times"></i></span>
        </li>
        </ul>
    </div>
</template>
<script>
export default {
    props: ["props"],
    methods: {
        passRemove(idx) {
            this.$emit("passRemove", idx);
        },
        passStatus(idx, action) {
            this.$emit("passStatus", idx, action);
        }
    }    
}
</script>
<style scoped>
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
  .nodata {
    width: 100%;
    padding-top: 70px;
    text-align: center;
    color: #999;
  }
</style>