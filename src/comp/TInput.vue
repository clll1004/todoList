<template>
  <div>
    <input type="text" v-model="todoItem" title="Todo" placeholder="Input Todo" @keyup.enter="passItem" />
    <button type="button" @click="passItem">Submit</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItem: ''
    }
  },
  methods: {
    passItem() {
      this.$emit('passItem', this.todoItem);
      this.todoItem = '';
    }
  }
}
</script>

<style scoped>
  input[type='text'] {
    width: calc(100% - 100px);
    padding: 10px 15px;
    border: 1px solid #ddd;
    box-sizing: border-box;
    border-radius: 10px 0 0 10px;
    outline: none;
    color: #666;
  }
  button {
    width: 100px; height: 38px;
    border-radius: 0 10px 10px 0;
    background: #fff;
    border: 1px solid #ddd;
    border-left: 0;
    box-sizing: border-box;
    outline: none;
    cursor: pointer;
  }
</style>
