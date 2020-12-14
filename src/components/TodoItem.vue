<template>
  <li
    class="todo-item"
    :class="{
      'todo-item--completed': todo.completed,
      'todo-item--editing': todo.editing
    }"
  >
    <div class="todo-item__body">
      <label class="todo-item__complete">
        <input
          v-model="todo.completed"
          @change="$emit('update-state')"
          class="todo-item__complete-checkbox"
          type="checkbox"
        >
        <span class="todo-item__complete-circle"></span>
      </label>
      <p
        @dblclick="$emit('edit-todo', todo.id)"
        class="todo-item__title"
      >{{todo.title}}</p>
      <div class="todo-item__wrapper-remove">
        <button
          @click="$emit('remove-todo', todo.id)"
          class="todo-item__remove"
        >
          <svg class="todo-item__remove-svg" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path _ngcontent-lfe-c7="" d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12 19 6.41z"></path></svg>
        </button>
      </div>
    </div>
    <input
      v-model="todo.title"
      @input="$emit('update-state')"
      @keyup.enter="$emit('done-todo-edit', todo.id)"
      @blur="$emit('done-todo-edit', todo.id)"
      v-todo-focus="todo.editing"
      class="input todo-item__edit"
      type="text"
    >
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  directives: {
    'todo-focus': function(element, binding) {
      if (binding.value) {
        element.focus()
      }
    }
  }
}
</script>

<style>
.todo-item {
  padding: 16px 0;
}

.todo-item__body {
  position: relative;
  display: flex;
  align-items: center;
}

.todo-item__complete {
  width: 60px;
  flex: 0 0 auto;
}

.todo-item__complete-checkbox {
  position: absolute;
  opacity: 0;
}

.todo-item__complete-circle {
  position: relative;
  display: block;
  margin: 0 auto;
  width: 20px;
  height: 20px;
  border: 2px solid #5f6368;
  border-radius: 50%;
  transition: border-color ease 280ms;
}

.todo-item__complete-circle::before {
  content: '';
  position: absolute;
  left: -2px;
  right: -2px;
  top: -2px;
  bottom: -2px;
  transform: scale(0.001);
  background: #1a73e8;
  border-radius: 50%;
  transition: transform ease 280ms;
}

.todo-item__complete-circle::after {
  content: '';
  position: absolute;
  left: -10px;
  right: -10px;
  top: -10px;
  bottom: -10px;
  background: #000;
  opacity: 0;
  border-radius: 50%;
  pointer-events: none;
  transition: opacity 0ms cubic-bezier(0, 0, .2, 1);
}

.todo-item__complete-circle:hover::after {
  opacity: .04;
}

.todo-item__complete-checkbox:checked + .todo-item__complete-circle {
  border-color: #1a73e8;
}

.todo-item__complete-checkbox:checked + .todo-item__complete-circle::before {
  transform: scale(0.5);
}

.todo-item--completed .todo-item__title {
  text-decoration: line-through;
}

.todo-item__title {
  flex: 1 1 auto;
  font-size: 28px;
}

.todo-item__wrapper-remove {
  width: 60px;
  flex: 0 0 auto;
}

.todo-item__remove {
  position: relative;
  display: block;
  margin: 0 auto;
}

.todo-item__remove::after {
  content: '';
  position: absolute;
  left: -8px;
  right: -8px;
  top: -8px;
  bottom: -8px;
  background: #000;
  opacity: 0;
  pointer-events: none;
  border-radius: 50%;
}

.todo-item__remove:hover::after {
  opacity: .04;
}

.todo-item__remove-svg {
  display: block;
  fill: #5f6368;
}

.todo-item__remove:hover .todo-item__remove-svg {
  fill: #174ea6;
}

.todo-item .todo-item__edit {
  display: none;
}

.todo-item--editing .todo-item__body {
  display: none;
}

.todo-item--editing .todo-item__edit {
  display: block;
}
</style>