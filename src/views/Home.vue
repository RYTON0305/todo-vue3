<template>
  <main class="main">
    <div class="container">
      <h1 class="header">Vue 3 TODO</h1>
      <todo-add :todo-id="todos.length" @add-todo="addTodo"></todo-add>
      <todo-filter
        :filter="filter"
        @change-filter="filter = $event"
      ></todo-filter>
      <todo-list :todos="filteredTodos"></todo-list>
    </div>
  </main>
</template>

<script>
// @ is an alias to /src
import TodoFilter from '@/components/TodoFilter'
import TodoAdd from '@/components/TodoAdd'
import TodoList from '@/components/TodoList'
import useTodos from '@/composables/useTodos'
import useFilteredTodos from '@/composables/useFilteredTodos'

export default {
  name: 'Home',
  components: {
    TodoFilter,
    TodoAdd,
    TodoList
  },
  setup() {
    const { todos, addTodo } = useTodos()

    const { filter, filteredTodos } = useFilteredTodos(todos)

    return {
      todos,
      addTodo,

      filter,
      filteredTodos
    }
  }
}
</script>

<style lang="stylus" scoped>
.main {
  width: 100vw;
  min-height: 100vh;
  padding: 10vh 0;
  display: flex;
  justify-content: center;
  align-items: start;
  background-color: rgb(203, 210, 240);
}

.container {
  width: 60%;
  min-width: 400px;
  box-shadow: 0 0 24px rgba(0 0 0, 0.15);
  border-radius: 24px;
  padding: 48px 28px;
  background-color: #f5f6fc;
}

.header {
  margin: 24px 0;
  font-size: 28px;
  color: #414873;
}
</style>
