<template>
  <form
    @submit.prevent="$emit('add-todo')"
    class="form-todo"
  >
    <input
      v-model="title"
      @input="$emit('update-title', title), $emit('update-state')"
      class="input form-todo__input"
      type="text"
      autocomplete="off"
      placeholder="What needs to be done?"
    >
    <button class="form-todo__add">
      <svg class="form-todo__add-svg" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path _ngcontent-lfe-c7="" d="M13,7h-2v4H7v2h4v4h2v-4h4v-2h-4V7z M12,2C6.48,2,2,6.48,2,12s4.48,10,10,10s10-4.48,10-10S17.52,2,12,2z M12,20 c-4.41,0-8-3.59-8-8s3.59-8,8-8s8,3.59,8,8S16.41,20,12,20z"></path></svg>
    </button>
  </form>
</template>

<script>
export default {
  props: ['title']
}
</script>

<style>
.form-todo {
  position: relative;
  margin-bottom: 15px;
}

.form-todo .form-todo__input {
  padding-right: 50px;
}

.form-todo__add {
  position: absolute;
  top: 50%;
  right: 20px;
  transform: translateY(-50%);
}

.form-todo__add-svg {
  display: block;
  fill: #5f6368;
}

.form-todo__add::after {
  content: '';
  position: absolute;
  left: -8px;
  right: -8px;
  top: -8px;
  bottom: -8px;
  pointer-events: none;
  background: #000;
  opacity: 0;
  border-radius: 50%;
}

.form-todo__add:hover .form-todo__add-svg {
  fill: #174ea6;
}

.form-todo__add:hover::after {
  opacity: .04;
}
</style>