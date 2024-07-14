<script setup>
import { Icon } from '@iconify/vue'

const props = defineProps({
  todoList: {
      required: true,
  }
})
defineEmits(["toggle-complete" , "toggle-edit" , "toggle-complete-todo" , "toggle-delete"])
</script>

<template>
  <div dir="rtl" class="main">

    <table>
      <thead>
        <tr>
          <th>ردیف</th>
          <th>وضعیت</th>
          <th>نام</th>
          <th>کارت</th>
          <th>امتیاز</th>
          <th>روز</th>
          <th>تاریخ</th>
          <th>عملگر</th>
        </tr>
      </thead>
      <tbody v-for="(user , index) in todoList">
        <tr>
              <td>
                <p>{{ index + 1 }}</p>
              </td>
              <td>
                <input type="checkbox" :checked="user.isCompleted" @input="$emit('toggle-complete' , index)">
              </td>

              <td v-show="user.isEditing">
                <input class="textedit" type="text" v-model="user.name">
              </td>
              <td v-show="user.isEditing">
                <input class="numedit" type="number" v-model="user.card">
              </td>
              <td v-show="user.isEditing">
                <input class="numedit" type="number" v-model="user.card">
              </td>
              <td v-show="user.isEditing">
                <input class="numedit" type="number" v-model="user.day">
              </td>
              <td v-show="user.isEditing">
                <input type="text" v-model="user.date">
              </td>

                
              <td v-show="! user.isEditing">
                <span class="show" :class="{'completed-todo' : user.isCompleted}">{{ user.name }}</span>
              </td>
              <td v-show="! user.isEditing">
                <span class="show" :class="{'completed-todo' : user.isCompleted}">{{ user.card }}</span>
              </td>
              <td v-show="! user.isEditing">
                <span class="show" :class="{'completed-todo' : user.isCompleted}">{{ user.gift }}</span>
              </td>
              <td v-show="! user.isEditing">
                <span class="show" :class="{'completed-todo' : user.isCompleted}">{{ user.day }}</span>
              </td>              
              <td v-show="! user.isEditing">
                <span class="show" :class="{'completed-todo' : user.isCompleted}">{{ user.date }}</span>
              </td>



            <td class="todo-actions">
              <Icon class="icon" v-if="user.isEditing" @click="$emit('toggle-complete-todo' , index)" icon="ph:check-circle" color="#41b080" width="22"/>
              <Icon class="icon" v-else @click="$emit('toggle-edit' , index)" icon="ph:pencil-fill" color="#41b080" width="22" />
              <Icon class="icon" icon="ph:trash" color="#f95e5e" width="22" @click="$emit('toggle-delete' , user.id)" />
            </td>

        </tr>
      </tbody>
    </table>

  </div>

</template>


<style lang="scss" scoped>

@font-face {
  font-family: 'BTitrBold';
  src: url('../assets/fonts/B\ Titr\ Bold_0.ttf') format('truetype');
  font-weight: bold;
  font-style: normal;
}

li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

    &:checked {
      background-color: #41b080;
    }
  }

  .todo {
    flex: 1;

    .completed-todo{
        text-decoration: line-through;
    }

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #41b080;
    }
    .show{
      margin-right: 20px;
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
input{
text-align: center
}
.numedit{
  width:40px;
}
table {
  width: 750px; /* عرض جدول */
}

th, td {
  border-radius: 5px;
  padding: 10px; /* پدینگ داخلی برای هر سلول */
  text-align: center; /* مرکز چین متن */
  border: 1px solid #ccc; /* حاشیه‌های سلول‌ها */
}
th {
  background-color: #f2f2f2; /* پس زمینه هدر */
}
.main{
  display: flex;
  flex-direction: column;
  align-self: center;
  font-family: 'BTitrBold';
}
th:nth-child(5), td:nth-child(5), 
th:nth-child(2), td:nth-child(2),
th:nth-child(4), td:nth-child(4),
th:nth-child(1), td:nth-child(1)
{
  width:10px;
}




</style>