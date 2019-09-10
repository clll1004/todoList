<template>
  <div>
    {{month}}.{{date}}.{{day}}
  </div>
</template>
<script>
  export default {
    data() {
      return {
        date: new Date().getDate() >= 10 ? new Date().getDate() : '0' + new Date().getDate(),
        month: (new Date().getMonth() + 1) >= 10 ? (new Date().getMonth() + 1) : '0' + (new Date().getMonth() + 1),
        day: new Date().getDay()
      }
    },
    beforeMount() {
      switch (this.day) {
        case 1: this.day = '월'; break;
        case 2: this.day = '화'; break;
        case 3: this.day = '수'; break;
        case 4: this.day = '목'; break;
        case 5: this.day = '금'; break;
        case 6: this.day = '토'; break;
        case 7: this.day = '일'; break;
        default: break;
      }
    }
  }
</script>
<style scoped>
  div {
    padding-bottom: 15px;
  }
</style>
