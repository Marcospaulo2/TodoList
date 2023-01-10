<template>
  <div id="app">
    <div class="container grid-xs py-5 ">
      <img class="img-responsive img-logo px-20" src="@/assets/logo.png" alt="image">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group py-3">
          <input type="text" v-model="todo.description" class="form-input" placeholder="Novo todo">
          <button class="btn btn-primary input-group-btn">adicionar</button>
          
        </div>
      </form>
      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todo="t"  />
       
      </div>
    </div>
  </div>
</template>

<script>

import Todo from './components/Todo'

export default {
  name: "app",
  components: {Todo},
  data() {
    return {todos: [], todo: { checked: false }  };
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now()
      this.todos.push(todo)
      this.todo = { checked: false};
    },

    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1) {
        const checked = !this. todos[index].checked
        this.$set(this.todos, index, {...this.todos[index], checked});
      }
    },

    removeTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1 ) {
        this.$delete(this.todos, index);
      }
    }
  }
};
</script>

<style scoped>
.img.logo {
  max-width: 200px;
  margin: 0 auto;
}
.todo-list {
  padding-top: 2rem;
}


</style> 
