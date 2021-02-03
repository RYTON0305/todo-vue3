<template>
  <div class="todo-list-item" :class="{ done: todoItem.completed }">
    <label class="label">
      <input
        class="checkbox"
        :checked="todoItem.completed"
        type="checkbox"
        @click="$emit('change-state', $event)"
      />
      <div class="note">{{ todoItem.content }}</div>
      <span class="check-btn"></span>
    </label>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todoItem: {
      type: Object,
      require: true
    }
  },
  setup(props) {
    return {}
  }
}
</script>

<style scoped lang="stylus">
.todo-list-item {
  background: #fff;
  padding: 16px;
  border-radius: 8px;
  color: #626262;

  &.done {
    .check-btn::after {
      opacity: 1;
    }

    .note {
      text-decoration: line-through;
      font-style: italic;
    }
  }

  .label {
    position: relative;
    display: flex;
    align-items: center;
    cursor: pointer;
  }

  .note {
    user-select: none;
  }

  .checkbox {
    margin-right: 16px;
    opacity: 0;
  }

  .check-btn {
    position: absolute;
    top: 0;

    &::before {
      border: 1px solid #b382f9;
    }

    &::after {
      transition: 0.4s;
      background: #b382f9;
      transform: translate(1px, 1px) scale(0.8);
      opacity: 0;
    }

    &::before {
      content: '';
      display: block;
      position: absolute;
      width: 18px;
      height: 18px;
      border-radius: 50%;
    }

    &::after {
      content: '';
      display: block;
      position: absolute;
      width: 18px;
      height: 18px;
      border-radius: 50%;
    }
  }
}
</style>
