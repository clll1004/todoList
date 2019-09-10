<template>
    <div class="date_area">
        <em>{{(today.getDate() >= 10) ? today.getDate() : '0' + today.getDate() }}</em>
        <p>{{(calcMonth >= 10) ? calcMonth : '0' + calcMonth}} {{today.getFullYear()}}</p>
        <span class="day">{{calcDay}}</span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            today: new Date(),
            calcMonth: '',
            calcDay: ''
        }
    },
    beforeMount() {
        this.calcMonth = this.today.getMonth() + 1;
        if (this.calcMonth === 1) { this.calcMonth = '1' }
        else if (this.calcMonth === 2) { this.calcMonth = '2' }
        else if (this.calcMonth === 3) { this.calcMonth = '3' }
        else if (this.calcMonth === 4) { this.calcMonth = '4' }
        else if (this.calcMonth === 5) { this.calcMonth = '5' }
        else if (this.calcMonth === 6) { this.calcMonth = '6' }
        else if (this.calcMonth === 7) { this.calcMonth = '7' }
        else if (this.calcMonth === 8) { this.calcMonth = '8' }
        else if (this.calcMonth === 9) { this.calcMonth = '9' }
        else if (this.calcMonth === 10) { this.calcMonth = '10' }
        else if (this.calcMonth === 11) { this.calcMonth = '11' }
        else { this.calcMonth = '12' }
        this.calcDay = this.today.getDay();
        if (this.calcDay === 1) { this.calcDay = '월' }
        else if (this.calcDay === 2) { this.calcDay = '화' }
        else if (this.calcDay === 3) { this.calcDay = '수' }
        else if (this.calcDay === 4) { this.calcDay = '목' }
        else if (this.calcDay === 5) { this.calcDay = '금' }
        else if (this.calcDay === 5) { this.calcDay = '토' }
        else { this.calcDay = '일' }
    }
}
</script>

<style scoped>
    .date_area { 
        overflow: hidden;
        padding-bottom: 15px;
        border-bottom: 1px solid #e6e6e6;
        color: #666;
    }
    p {
        float: left;
        width: 40px;
        margin-top: 2px;
        font-size: 13px;
    }
    em {
        float: left;
        margin-right: 4px;
        font-size: 37px;
        font-weight: bold;
        font-style: normal;
        vertical-align: top;
        line-height: 1;
    }
    .day {
        float: right;
        font-size:13px;
    }
</style>
