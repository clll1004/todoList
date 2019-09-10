<template>
    <form>
        <fieldset>
            <legend>TODO INPUT</legend>
            <p>
                <span class="imp">*</span>
                <input type="text" id="todo" v-model="newTodo.title" @keyup="checkFill" placeholder="INPUT TODO" autofocus autocomplete="off" />
                <label for="todo">할 일을 입력하세요.</label>
            </p>
            <p v-if="isShow">
                <select v-model="newTodo.time">
                    <option value="x">Select Hour</option>
                    <option value="00">~ 00:00</option>
                    <option value="01">~ 01:00</option>
                    <option value="02">~ 02:00</option>
                    <option value="03">~ 03:00</option>
                    <option value="04">~ 04:00</option>
                    <option value="05">~ 05:00</option>
                    <option value="06">~ 06:00</option>
                    <option value="07">~ 07:00</option>
                    <option value="08">~ 08:00</option>
                    <option value="09">~ 09:00</option>
                    <option value="10">~ 10:00</option>
                    <option value="11">~ 11:00</option>
                    <option value="12">~ 12:00</option>
                    <option value="13">~ 13:00</option>
                    <option value="14">~ 14:00</option>
                    <option value="15">~ 15:00</option>
                    <option value="16">~ 16:00</option>
                    <option value="17">~ 17:00</option>
                    <option value="18">~ 18:00</option>
                    <option value="19">~ 19:00</option>
                    <option value="20">~ 20:00</option>
                    <option value="21">~ 21:00</option>
                    <option value="22">~ 22:00</option>
                    <option value="23">~ 23:00</option>
                </select>
                <input type="text" id="place" v-model="newTodo.place" placeholder="INPUT PLACE" autocomplete="off" />
                <label for="place">위치를 입력하세요.</label>
            </p>
            <button type="button" class="btn_more" @click="toggleMore"><i class="fa" :class="isShow ? 'fa-caret-up' : 'fa-caret-down'"></i></button>
            <button type="button" class="btn_add" @click="passItem" :disabled='isDisabled'>ADD</button>
        </fieldset>
    </form>
</template>

<script>
export default {
    data() {
        return {
            newTodo: {
                title: '',
                time: 'x',
                place: '',
            },
            isShow: true,
            isDisabled: true
        }
    }, 
    methods: {
        passItem(event) {
            event.preventDefault()
            this.$emit('passItem', this.newTodo);
            this.clearTodo();
        },
        toggleMore() {
            this.isShow = !this.isShow;
            this.newTodo.time = 'x';
            this.newTodo.place = '';
        },
        clearTodo() {
            this.newTodo = {
                title: '',
                time: 'x',
                place: '',
                important: false
            }
            this.isDisabled = true;
        },
        checkFill() {
            this.isDisabled = this.newTodo.title === '';
        }
    }
}
</script>

<style scoped>
    form {
        position: relative;
        margin: 20px 0;
        border-radius: 3px;
        box-sizing: border-box;
        border: 1px solid #ddd;
        background: #fff;
        overflow: hidden;
    }
    fieldset {
        border: none;
    }
    legend {
        display: none;
    }
    p {
        position: relative;
        width: 95%;
        height: 40px;
        padding: 0 15px; 
        box-sizing: border-box;
    }
    p .imp {
        position: absolute;
        top: 33%; left: 15px;
        color: #fa9c9c;
    }
    p:last-of-type input[type='text'] {
        border-bottom: none;
    }
    input[type='text'] {
        width: 100%;
        height: 100%;
        padding: 0 15px;
        border: none;
        border-bottom: 1px dashed #ddd;
        box-sizing: border-box;
        outline: none;
        color: #666;
        font-size: 11px;
    }
    input[type='text'] + label {
        display: none;
    }
    input[type='checkbox'] {
        margin: 14px 5px 14px 15px;
    }
    label {
        color: #666;
        font-size: 12px;
        line-height: 40px;
        vertical-align: top;
        cursor: pointer;
    }
    input[type='text']#place {
        width: calc(100% - 100px);
    }
    select{
        display: inline-block;
        width: 100px;
        padding: 3px;
        border: 1px solid #ddd;
        border-radius: 3px;
        color: #666;
        font-size: 12px;
    }
    .btn_more {
        position: absolute;
        right: 10px; top: 0;
        width: 12px; height: calc(100% - 40px);
        border: none;
        background: none;
        color: #333;
        cursor: pointer;
        outline: none;
    }
    .btn_more:hover, .btn_more:active {
        color: #fa9c9c;
    }
    .btn_more i.fa-caret-up {
        color: #fa9c9c;
    }
    .btn_add {
        width: 100%;
        height: 40px;
        color: #f9f9f9;
        font-weight: bold;
        border: none;
        box-sizing: border-box;
        background: #fa9c9c;
        cursor: pointer;
        outline: none;
    }
    .btn_add:hover {
        color: #fff;
        background: #f39494;
    }
    .btn_add:disabled,.btn_add:disabled:hover {
        color: #f9f9f9;
        background: #ddd;
        cursor: auto;
    }
</style>
