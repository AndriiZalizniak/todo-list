<template>
  <div>
    <ul>
      <todo-item 
        v-for="(tElem, i) of varTodo"
        v-bind:todo="tElem"
        v-bind:index="i"
        v-on:remove-li="removeLi"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
  props: ['varTodo'],
  components: {
    'todo-item': TodoItem
  },
  methods: {
    removeLi(id) {
      this.$emit('remove-li', id)
    }
  }
}
</script>

<style>
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
</style>
