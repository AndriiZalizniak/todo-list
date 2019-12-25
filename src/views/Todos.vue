<template>
  <div>
    <h2>Todo List</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <add-li-elem
      v-on:add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <!-- <loader v-if="loading"></loader> -->

    <!-- v-if="todoArray.length" -->
    <!-- v-if="filteredTodos.length" -->
    <!-- v-else-if="todoArray.length" -->
    <todo-list
      v-if="filteredTodos.length"
      v-bind:varTodo="filteredTodos"
      v-on:remove-li="removeLi"
    />
    <p v-else>NO list</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import AddLiComponent from '@/components/AddLiComponent.vue'
import Loader from '@/components/Loader.vue'

export default {
  name: 'app',
  data() {
    return {
      todoArray: [
        {
          id: 1,
          title: 'title 1',
          completed: false
        },
        {
          id: 2,
          title: 'title 2',
          completed: false
        },
        {
          id: 3,
          title: 'title 3',
          completed: false
        }
      ],
      loading: true,
      filter: 'all'
    }
  },
  // mounted(){
  //   fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
  //   .then(response => response.json())
  //   .then(json => {
  //     setTimeout(() => {
  //       this.todoArray = json
  //       this.loading = false
  //     }, 500)
  //   })
  // },
  // watch: {
  //   filter(value) {
  //     console.log(value);
  //   }
  // },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todoArray
      }

      if (this.filter === 'completed') {
        return this.todoArray.filter(t => t.completed)
      }

      if (this.filter === 'not-completed') {
        return this.todoArray.filter(t => !t.completed)
      }
    }
  },
  methods: {
    removeLi(id) {
      this.todoArray = this.todoArray.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todoArray.push(todo)
    }
  },
  components: {
    'todo-list': TodoList,
    'add-li-elem': AddLiComponent,
    'loader': Loader
  }
}
</script>
