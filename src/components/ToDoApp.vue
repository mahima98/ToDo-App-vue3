<template>
  <div class="container px-8">
    <h1 class="test text-red-400 underline py-8">My Todo App</h1>
    <div class="form-container ">
      <form class="flex flex-col gap-2" @submit.prevent="addNewToDo">
        <label>Add new Todo</label>
        <input v-model="newTodo"  name="newTodo" class="border border-gray-200 rounded-md h-8 px-4"/>
        <button  type="button" id="addToDo" ref="addToDo" class="bg-blue-300 px-4 py-2 rounded-md">Add New Todo</button>
        <button @click="markAllDone()" class="bg-teal-300 px-4 py-2 rounded-md">Mark all done</button>
        <button @click="removeAll()" class="bg-red-300 px-4 py-2 rounded-md">Remove all toDos</button>
      </form>

      <ul>
        <li v-for="(todo, index) in todoList" :key="todo.id" :value="index">
            <h3 :class="{ 'line-through bg-red-400' : todo.done }" @click="toggleDone(todo)" class="text-md my-2 mx-2 px-4 py-2 bg-orange-300 rounded-md inline-block"> {{todo.content}}</h3>
            <button @click="removeTodo(index)" class="bg-blue-300 px-2 text-xs rounded-md py-1">Remove todo</button>
        </li>
      </ul>
   </div>
  </div>
</template>
<script>  
import {ref} from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todoList = ref([]);

    //To do, disable button when input field is empty

    function addNewToDo() {
        if(newTodo.value !== '')
        {
        todoList.value.push({
          id: Date.now(),
          done: false,
          content: newTodo.value
        })
        }

        // clear text entered as input
        newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function removeTodo(index) {
      todoList.value.splice(index, 1)
    }

    function markAllDone() {
      todoList.value.forEach((todo) => todo.done = true)
    }

    function removeAll() {
      todoList.value = []
    }

    return {
      addNewToDo,
      newTodo,
      todoList,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll
    }
  },
}
</script>