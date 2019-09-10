<template>
    <footer>
        <div class="btns">
            <button type="button" @click="paddDoneAll">DONE ALL!</button>
            <button type="button" @click="passClear">CLEAR ALL!</button>
        </div>
        <p><b>TOTAL TODOS:</b> {{ propsTotalCount }}</p>
        <p><b>COMPLETE TODOS:</b> {{ propsCompleteCount }}</p>
    </footer>
</template>

<script>
export default {
    props: ['propsTotalCount', 'propsCompleteCount'],
    methods: {
        paddDoneAll() {
            this.$emit('passDoneAll');
        },
        passClear() {
            this.$emit('passClear');
        }
    }
}
</script>

<style scoped>
    footer {
        margin-top: 30px;
    }
    .btns {
        overflow: hidden;
        margin-bottom: 30px;
    }
    .btns button {
        width: 48%;
        height: 40px;
        margin-right: 4%;
        border: none;
        border-radius: 3px;
        font-weight: bold;
        color: #f9f9f9;
        background: #fa9c9c;
        cursor: pointer;
        outline: none;
    }
    .btns button:hover {
        color: #fff;
        background: #f39494;
    }
    .btns button:last-child {
        margin-right: 0;
        background: rgba(0,0,0,.3);
    }
    .btns button:last-child:hover {
        background: rgba(0,0,0,.4);
    }
    p {
        line-height: 20px;
        font-size: 11px;
        color: #666;
    }
</style>
