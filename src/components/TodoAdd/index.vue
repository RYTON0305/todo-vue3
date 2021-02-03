<template>
  <div class="input-box">
    <input
      type="text"
      class="input-box-input"
      v-model="todoContent"
      @keyup.enter="emitAddTodo"
    />
    <button class="input-box-btn" @click="emitAddTodo">
      <i class="plus"></i>
    </button>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'TodoAdd',
  props: {
    todoId: Number
  },
  setup(props, context) {
    return userEmitAddTodo(props.todoId, context.emit)
  }
}

function userEmitAddTodo(todoId, emit) {
  const todoContent = ref('')
  const emitAddTodo = () => {
    const todo = {
      id: todoId,
      content: todoContent.value,
      completed: false
    }
    emit('add-todo', todo)
    todoContent.value = ''
  }
  return {
    todoContent,
    emitAddTodo
  }
}
</script>

<style scoped lang="stylus">
.input-box {
  position: relative;
  display: flex;
  align-items: center;

  &-input {
    padding: 16px 52px 16px 18px;
    border-radius: 48px;
    border: none;
    outline: none;
    box-shadow: 0 0 24px rgba(0 0 0, 0.08);
    width: 100%;
    font-size: 16px;
    color: #626262;
  }

  &-btn {
    width: 46px;
    height: 46px;
    border-radius: 50%;
    background: linear-gradient(#c0a5f3, #7f95f7);
    border: none;
    color: #fff;
    position: absolute;
    right: 0;
    cursor: pointer;
    outline: none;

    .plus {
      display: block;
      width: 100%;
      height: 100%;
      background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
      background-size: 50% 2px, 2px 50%;
      background-position: 50%;
      background-repeat: no-repeat;
    }
  }
}
</style>
