<script>
  import JSConfetti from 'js-confetti'  
  const confetti = new JSConfetti()

  let id = 0  
  export default {
    data() {
      return {
        newTodo: '',
        filterType: 'All',
        emptyField: false,
        todos: [
          { id: id++, text: 'Learn HTML', done: true },
          { id: id++, text: 'Learn JavaScript', done: true },
          { id: id++, text: 'Learn Vue', done: false }
        ]        
      }
    },
    computed: {
    filteredTodos() {
      if (this.filterType == 'Active') {
        return this.todos.filter((t) => t.done == false)
      }
      else if (this.filterType == 'Completed') {
        return this.todos.filter((t) => t.done == true)
      }
      else {
        return this.todos
      }
    }
  },
    methods: {
      addTodo() {
        if (this.newTodo.trim().length != 0) {
          this.todos.push({ id: id++, text: this.newTodo, done: false })     
          this.newTodo = '' 
          this.emptyField = false            
        }        
        else {
          this.emptyField = true
        }
      },
      removeTodo(todo) {
        this.todos = this.todos.filter((t) => t !== todo)
        this.checkIfAllCompleted()
      },
      checkIfAllCompleted() {
        let startStatus = true
        this.emptyField = false  
        this.todos.forEach(function callback(item) {
          if (item.done != true) {
            startStatus = false
          }
        })
        if (startStatus == true) {
          confetti.addConfetti()
        }
      }
    }
  }
</script>
<template>
  <div class="filter">
    <button class="filter_button" :class="{filter_button__selected: (this.filterType == 'All')}" @click="filterType = 'All'">
    All
    </button>
    <button class="filter_button" :class="{filter_button__selected: (this.filterType == 'Active')}" @click="filterType = 'Active'">
      Active
    </button>
    <button class="filter_button" :class="{filter_button__selected: (this.filterType == 'Completed')}" @click="filterType = 'Completed'">
      Completed
    </button>
  </div>

  <div class="tablet">
    <div class="input-container">
      <form class="todo_form" @submit.prevent="addTodo">
        <input class="todo_input" v-model="newTodo" maxlength="40"/>
        <button class="todo_button">Add Todo</button>
      </form>
      <p class="red-error" v-if="emptyField">The task name cannot be empty</p>
    </div>    
    
    <ul class="list">
      <li class="task" v-for="todo in this.filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" @change="checkIfAllCompleted" placeholder="Input your task">
        <span class="task_text" :class="{ done: todo.done }">{{ todo.text }}</span>
        <button class="task_buttom" @click="removeTodo(todo)">X</button>
      </li>
    </ul>
  </div>  
</template>
<style>
.done {
  text-decoration: line-through;
}
.input-container {
  position: sticky;
  top: 0;
  background-color: white;
  z-index: 2;
}
.todo_form {  
  width: 100%;
  padding-top: 20px;
}
.todo_input {
  width: 70%;
  height: 40px ;
  padding-left: 10px;
  margin-right: 0px;
  border-color: black;
  border-top-left-radius: 15px;
  border-bottom-left-radius: 15px;
  outline: none;
}
.todo_button {
  width: 20%;
  height: 40px ;
  margin: 10px;
  margin-left: -2px;
  border-color: black;
  border-top-right-radius: 15px;
  border-bottom-right-radius: 15px;
}
.red-error {
  color: red;
}
.list {
  list-style: none;
  padding: 20px;
  text-align: left
}
.task {
  padding-bottom: 10px;
}
.task_text {
  padding-left: 10px;
  padding-right: 10px;
  padding-bottom: 5px;
}
.task_button {
  padding-right: 10px;
}
.tablet {
  text-align: center;
  border: solid;
  border-width: 2px;
  border-color: black;
  border-top: none;
}
.filter {
  position: sticky;
}
.filter_button {
  height: 50px;
  background-color: rgba(0, 0, 0, 0);
  border-color: black;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  width: 30%;
}
.filter_button__selected {
  width: 40%;
  border-color: black;
  border-bottom: none;  
}
</style>
