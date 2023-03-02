<script>
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Learn HTML', done: true },
        { id: id++, text: 'Learn JavaScript', done: true },
        { id: id++, text: 'Learn Vue', done: false }
      ]
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  
  <ul>
    <div class="myclass">
      <li :class="{ done: todo.done }" v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.done">
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button class="delete" @click="removeTodo(todo)">delete</button>
      </li>
    </div>
  </ul>
  
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
div.myclass{
  text-align: center;
  align-items: center;
}

li{
    background-color: rgba(235, 124, 124, 0.23);
    box-shadow: 0 5px 37px -1px rgba(51, 51, 51, 0.23);
    align-items: center;
    text-align: center;
    padding: 10px;
    list-style-type: none;
    border-radius: 10px;
    height: 60PX;
    margin-top: 5px;
}
li:hover{
    transform: scale(1.2);
    box-shadow: 0 9px 47px 11px rgba(51, 51, 51, 0.18);
}
li.done{
  background-color: rgba(133, 36, 236, 0.23);
}
ul{
  text-align: center;
  margin-top: 20px;
}
button.delete{
  background-color: rgba(243, 10, 10, 0.503);
  border-radius: 10px;
  position: relative;
  left: 5px;
}
button.delete:hover {
  transform: scale(1.2);
  background-color: red;
}
</style>