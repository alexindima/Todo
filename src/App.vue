<!-- 1/15 
<template>
  <h1>Hello World!</h1>
</template>
-->

<!-- 2/15
<script>
  export default {
    data() {
      return {
        message: 'Hello World!'
      }
    }
  }
</script>
<template>
  <h1>{{ message }}</h1>
</template>-->

<!-- 3/15
<script>
  export default {
    data() {
      return {
        titleClass: 'title'
      }
    }
  }
</script>    
<template>
  <h1 :class="titleClass">Make me red</h1>
</template>

<style>
.title {
  color: red;
}
</style>-->

<!--4/15
<script>
  export default {
    data() {
      return {
        count: 0
      }
    },
    methods: {
      increment() {
        this.count++
      }
    }
  }
</script>
<template>
  <button @click="increment">count is: {{ count }}</button>
</template>-->

<!--5/15
<script>
  export default {
    data() {
      return {
        text: ''
      }
    }
  }
</script>
<template>
  <input v-model="text" placeholder="Type here">
  <br>
  <p>{{ text }}</p>
</template>-->

<!--6/15
<script>
  export default {
    data() {
      return {
        awesome: true
      }
    },
    methods: {
      toggle() {
        this.awesome = !this.awesome
      }
    }
  }
</script>  
<template>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>-->

<!--7/15
<script>
  let id = 0  
  export default {
    data() {
      return {
        newTodo: '',
        todos: [
          { id: id++, text: 'Learn HTML' },
          { id: id++, text: 'Learn JavaScript' },
          { id: id++, text: 'Learn Vue' }
        ]
      }
    },
    methods: {
      addTodo() {
        this.todos.push({ id: id++, text: this.newTodo })
      },
      removeTodo(todo) {
        this.todos = this.todos.filter(text => text != todo)
        // ...
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
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>-->

<!--8/15
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
      if (this.hideCompleted == true) {
        return this.todos.filter((t) => t.done == false)
      }
      else {
        return this.todos
      }
      
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
    <input v-model="newTodo" />
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in this.filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>
<style>
.done {
  text-decoration: line-through;
}
</style>-->


<!--9/15
<script>
  export default {
    mounted() {
      this.$refs.p.textContent = "fsdfsdf"
    }
  }
</script>
<template>
  <p ref="p">hello</p>
</template>-->

<!--10/15
<script>
  export default {
    data() {
      return {
        todoId: 1,
        todoData: null
      }
    },
    methods: {
      async fetchData() {
        this.todoData = null
        const res = await fetch(
          `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
        )
        this.todoData = await res.json()
      }
    },
    mounted() {
      this.fetchData()
    },
    watch: {
      todoId(newID) {
        this.fetchData();
      }
    }
  }
</script>
<template>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>-->

<!--11/15
<script>
import ChildComp from './components/ChildComp.vue'
  export default {
    components: {
      ChildComp
    }
  }
</script>
<template>
  <ChildComp />
</template>-->

<!--12/15
<script>
  import ChildComp from './components/ChildComp.vue'  
  export default {
    props: {
      msg: String
    },
    components: {
      ChildComp
    },
    data() {
      return {
        greeting: 'Hello from parent'
      }
    }
  }
</script>
<template>
  <ChildComp :msg="greeting" />
</template>-->

<!--13/15
<script>
  import ChildComp from './components/ChildComp1.vue'  
  export default {
    components: {
      ChildComp
    },
    data() {
      return {
        childMsg: 'No child msg yet'
      }
    }
  }
</script>
<template>
  <ChildComp  @response="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>
</template>-->

<!--14/15
<script>
  import ChildComp from './components/ChildComp2.vue' 
  export default {
    components: {
      ChildComp
    },
    data() {
      return {
        msg: 'from parent'
      }
    }
  }
</script>
<template>
  <ChildComp>{{ msg }}</ChildComp>
</template>-->

<!--15/15-->
<script>
  import JSConfetti from 'js-confetti'  
  const confetti = new JSConfetti()
  
  export default {
    mounted() {
      this.showConfetti()
    },
    methods: {
      showConfetti() {
        confetti.addConfetti()
      }
    }
  }
  </script>  
  <template>
    <h1 @click="showConfetti">🎉 Congratulations!</h1>
  </template>  
  <style>
  h1 {
    text-align: center;
    cursor: pointer;
    margin-top: 3em;
  }
  </style>
