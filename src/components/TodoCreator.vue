<script setup>
import { defineEmits, reactive } from 'vue';
import moment from 'moment-jalaali'


const getTodayDate = () => {
  return moment().format('jYYYY/jM/jD')
}



const emit = defineEmits(['create-todo'])

const todoState = reactive({
    name:"",
    card: 0,
    day:4,
    date:getTodayDate(),
    invalid: null,
    errMsg:''
}) 

const createTodo = () => {

    todoState.invalid =null;

    if (todoState.name !== ""){

        emit('create-todo' , todoState.name , todoState.card , todoState.day , todoState.date);
        todoState.name = "";
        return
    }
    todoState.invalid = true;
    todoState.errMsg = "Todo value cannot be empty." 
}
</script>


<template>
    <div class="input-wrap" :class="{ 'input-err' : todoState.invalid }">

        <button @click="createTodo()">افزودن</button>
        <input name="name" type="text" v-model="todoState.name" placeholder="نام">
        <input name="name" type="number" v-model="todoState.card">
        <input name="name" type="number" v-model="todoState.day">

    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>

</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  justify-content: center;
  gap:5px;
  direction:rtl;

  input[type="text"] {
    width: 60%;
    padding: 8px 6px;
    border: 1px solid black;
    border-radius: 3px;
    border: none;
  }
  input[type="number"] {
    width: 10%;
    padding: 8px 6px;
    border: 1px solid black;
    border-radius: 3px;
    border: none;
  }


  button {
    padding: 8px 16px;
    border: none;
    border-radius: 3px;
}
}

.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>