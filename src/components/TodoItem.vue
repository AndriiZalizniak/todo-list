<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <label>
        <input type="checkbox" 
               v-on:change="todo.completed = !todo.completed">
        <strong>{{ index + 1 }}</strong>
        {{ todo.title | uppercase }}
      </label>
    </span>
    <button 
      type="button" 
      class="rm" 
      v-on:click="$emit('remove-li', todo.id)"
    >&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style>
  li {
    margin: 10px 0;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    border: 1px solid #ccc;
  }
  input {
    margin-right: 15px;
  }
  .done {
    text-decoration: line-through;
  }
  button {
    padding: 5px 10px;
    border-radius: 50%;
    outline: none;
    font-weight: bold;
  }
  label:hover {
    cursor: pointer;
  }
</style>
