<template>
    <main class="app">
      <section class="greeting">
        <h2 class="title">
          What's up, <input type="text" id="name" placeholder="Name here" v-model="nameData">
        </h2>
      </section>
  
      <section class="create-todo">
        <h3>CREATE A TODO</h3>
  
        <form id="new-todo-form" @submit.prevent="addTodo">
          <h4>New Task!</h4>
          <input 
            type="text" 
            name="content" 
            id="content" 
            placeholder="type your task here"
            v-model="input_content" />
          
          <h4>Pick a category</h4>
          <div class="options">
            <label>
              <input 
                type="radio" 
                name="category" 
                id="category1" 
                value="personal"
                v-model="input_category" />
              <span class="bubble personal"></span>
              <div>Personal</div>
            </label>
            <label>
              <input 
                type="radio" 
                name="category" 
                id="category2" 
                value="college"
                v-model="input_category" />
              <span class="bubble college"></span>
              <div>College</div>
            </label>
          </div>
  
          <input type="submit" value="Add todo" />
        </form>
      </section>
  
      <section class="todo-list">
        <h3>TODO LIST</h3>
        <div class="list" id="todo-list">
          <div v-for="todo in todos" :class="`todo-item ${todo.done ? 'done' : ''}`">
            <label>
              <input type="checkbox" v-model="todo.done" />
              <span :class="`bubble ${todo.category == 'personal' ? 'personal' : 'college'}`"></span>
            </label>
  
            <div class="todo-content">
              <input type="text" v-model="todo.content" />
            </div>
  
            <div class="actions">
              <button class="delete" @click="removeTodo(todo)">Delete</button>
            </div>
          </div>
        </div>
      </section>
    </main>
  </template>
  
  <script setup>
  import { ref, onMounted, computed, watch } from 'vue';
  
  const todosData = ref([]);
  const nameData = ref('');
  
  const input_content = ref('');
  const input_category = ref(null);
  
  const todos = computed(() => todosData.value.sort((a, b) => a.createdAt - b.createdAt));
  
  watch(nameData, (newVal) => {
    localStorage.setItem('name', newVal);
  });
  
  watch(todosData, (newVal) => {
    localStorage.setItem('todos', JSON.stringify(newVal));
  }, {
    deep: true,
  });
  
  const addTodo = () => {
    if (input_content.value.trim() === '' || input_category.value === null) {
      return;
    }
  
    todosData.value.push({
      content: input_content.value,
      category: input_category.value,
      done: false,
      editable: false,
      createdAt: new Date().getTime(),
    });
    input_content.value = '';
    input_category.value = null;
  };
  
  const removeTodo = (todo) => {
    todosData.value = todosData.value.filter((t) => t !== todo);
  };
  
  onMounted(() => {
    nameData.value = localStorage.getItem('name') || '';
    todosData.value = JSON.parse(localStorage.getItem('todos')) || [];
  });
  </script>
  
  <style>
  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .greeting {
    margin-bottom: 20px;
  }
  
  .title {
    font-size: 20px;
  }
  
  #create-todo {
    margin-bottom: 20px;
  }
  
  .create-todo,
  .todo-list {
    width: 100%;
    max-width: 500px;
  }
  
  .options {
    display: flex;
    justify-content: space-around;
    margin-bottom: 10px;
  }
  
  .todo-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .todo-item.done {
    background-color: #d4edda;
  }
  
  .bubble {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    display: inline-block;
    margin-right: 10px;
  }
  
  .bubble.personal {
    background-color: #1c1d1e;
  }
  
  .bubble.college {
    background-color: #f29f10;
  }
  </style>
  