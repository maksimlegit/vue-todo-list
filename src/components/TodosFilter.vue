<template>
  <div class="todos-filter">
    <button
      @click="$emit('update-filter', 'all'), $emit('update-state')"
      class="todos-filter__button"
      :class="{
        'todos-filter__button--active': value === 'all'
      }"
    >All</button>
    <button
      @click="$emit('update-filter', 'active'), $emit('update-state')"
      class="todos-filter__button"
      :class="{
        'todos-filter__button--active': value === 'active'
      }"
    >Active</button>
    <button
      @click="$emit('update-filter', 'completed'), $emit('update-state')"
      class="todos-filter__button"
      :class="{
        'todos-filter__button--active': value === 'completed'
      }"
    >Completed</button>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true
    }
  }
}
</script>

<style>
.todos-filter {
  display: flex;
}

.todos-filter__button {
  cursor: pointer;
  padding: 16px 16px 14px 16px;
  color: #1a73e8;
  font-weight: 500;
  font-size: 18px;
  border-bottom: 2px solid transparent;
}

.todos-filter__button:hover {
  background: rgba(26, 115, 232, .04);
}

.todos-filter__button--active {
  border-color: #1a73e8;
}
</style>