<script setup>
import TodoCreator from '../components/TodoCreator.vue';
import Todoitem from '../components/Todoitem.vue';
import {Icon} from '@iconify/vue';
import { ref  , watch , computed } from 'vue'
import { uid } from 'uid';

const todoList = ref([]);

watch( 
  todoList , 
  () => { 
    STLLS();
  } , 
  { 
    deep:true 
  } 
);

const todoComputed = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted )
})


const fetchTodoList = () => {

    let savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if(savedTodoList){
      todoList.value = savedTodoList;
    }
}

fetchTodoList();

const STLLS = () => {
  localStorage.setItem("todoList" , JSON.stringify(todoList.value))
}

const createTodos = (name , card , day , date) => {
  todoList.value.push({
    id: uid(),
    name,
    card,
    day,
    date,
    gift: card / 3 * 5 , 
    isCompleted: null,
    isEditing: null
  })
};

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
}

const toggleTodoEdit = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
}

const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
}

</script>

<template>
  <main>
    <h1>
      افزودن دانشجو
    </h1>
    <TodoCreator @create-todo="createTodos" />

    <ul class="todo-list" v-if="todoList.length > 0">
      <Todoitem  :todoList="todoList" @toggle-complete="toggleTodoComplete" @toggle-edit="toggleTodoEdit" @toggle-complete-todo="toggleTodoEdit" @toggle-delete="deleteTodo" />
    </ul>
    <p class="todos-msg" v-else >
      <Icon icon="noto-v1:sad-but-relieved-face"/> 
      <span>You dont have todo`s to complet ! add a one</span>
    </p>
    <p v-if="todoComputed && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper"/> 
      <span>You have completed all your todos !</span>
    </p>
  </main>
</template>


<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 30px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>