<template>
    <div class="wrapper">
        <div class="inputWrapper">
            <input v-model="state.inputValue" />
            <div class="addBtn" @click="handleAdd">ADD</div>
        </div>
        <h1>目前已有数量：{{computedNum}}</h1>
        <h1>当前是否有重复内容：{{ hasRepeatNum }}</h1>
        <h1></h1>
        <div class="item" v-for="(item, index) in state.todoList" :key="index">
            <span>{{item.message}}</span>
            <i @click="handleDel(index)"> x </i>
        </div>
    </div>
</template>

<script setup lang="ts">
import { reactive,ref, computed } from 'vue';
import { TodoListItem } from './interface';
    const state = reactive({
        inputValue: '',
        todoList: []
    })


    let hasRepeatNum = ref(0)

    const computedNum = computed(() => {
        return state.todoList.length === 0? '没有内容': `${state.todoList.length}个内容`
    })

    
    const handleAdd = () => {
        const newItem = {
            message: state.inputValue 
        }
        state.todoList.push(newItem)

        hasRepeatNum.value = state.todoList.filter((item:TodoListItem) => {
             return item.message === state.inputValue
        }).length
    }

    const handleDel = (index: number) => {
        state.todoList = state.todoList.filter((item: TodoListItem, itemIndex: number) => {
            return index!=itemIndex
        })
    }
</script>

<!-- <script lang="ts">
import { reactive, computed } from 'vue';
import { TodoListItem } from './interface';
export default {
    setup() {
        const state = reactive({
            inputValue: '',
            todoList: [],
            hasRepeat: false
        })

        const computedNum = computed(() => {
            return state.todoList.length === 0? '没有内容': `${state.todoList.length}个内容`
        })

        
        const handleAdd = () => {
            const newItem = {
                message: state.inputValue 
            }
            state.todoList.push(newItem)
        }

        const handleDel = (index: number) => {
            state.todoList = state.todoList.filter((item: TodoListItem, itemIndex: number) => {
                return index!=itemIndex
            })
        }

        return { 
            state,
            computedNum,
            handleAdd,
            handleDel
        }
    }
}
</script> -->
<style scoped>
.wrapper {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.inputWrapper {
    padding: 20px;
    box-sizing: border-box;
    align-self: stretch;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.inputWrapper input {
    flex: 1;
    border: 1px solid rgb(84, 82, 82);
    border-radius: 4px;
    line-height: 30px;
}
.inputWrapper .addBtn {
    color: #fff;
    background: skyblue;
    padding: 5px 15px;
    margin-left: 10px;
}

.item {
    align-self: stretch;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 4px;
}

.item span {
    font-size: 20px;
    line-height: 28px;
}
.item i {
    width: 30px;
    height: 30px;
    background: #ccc;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;;
    border-radius: 4px;
}
</style>