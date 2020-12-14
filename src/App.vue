<template>
  <header class="header">
    <form-todo
      :title="newTodoTitle"
      @update-title="newTodoTitle = $event"
      @update-state="updateState"
      @add-todo="addTodo"
    ></form-todo>
  </header>
  <main>
    <todo-list
      :todos="filteredTodos"
      @remove-todo="removeTodo($event)"
      @edit-todo="editTodo($event)"
      @done-todo-edit="doneTodoEdit($event)"
      @update-state="updateState"
    ></todo-list>
  </main>
  <footer>
    <todos-filter
      :value="todosFilterValue"
      @update-filter="todosFilterValue = $event"
      @update-state="updateState"
    ></todos-filter>
  </footer>
</template>

<script>
import FormTodo from '@/components/FormTodo'
import TodoList from '@/components/TodoList'
import TodosFilter from '@/components/TodosFilter'

export default {
  data() {
    const localStorageState = localStorage.getItem('state')
    if (localStorageState) {
      return JSON.parse(localStorageState)
    } else {
      return {
        newTodoTitle: '',
        nextTodoId: 1,
        todos: [],
        todosFilterValue: 'all'
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoTitle.trim()) {
        this.todos.push({
          id: this.nextTodoId++,
          title: this.newTodoTitle,
          completed: false,
          editing: false
        })
        this.newTodoTitle = ''
        this.updateState()
      }
    },
    removeTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
      this.updateState()
    },
    editTodo(id) {
      this.todos[this.todos.findIndex(todo => todo.id === id)].editing = true
      this.updateState()
    },
    doneTodoEdit(id) {
      this.todos[this.todos.findIndex(todo => todo.id === id)].editing = false
      this.updateState()
    },
    updateState() {
      localStorage.setItem('state', JSON.stringify(this.$data))
    }
  },
  computed: {
    filteredTodos() {
      switch (this.todosFilterValue) {
        case 'all':
          return this.todos
        case 'active':
          return this.todos.filter(todo => !todo.completed)
        case 'completed':
          return this.todos.filter(todo => todo.completed)
      }
    }
  },
  components: {
    FormTodo,
    TodoList,
    TodosFilter
  }
}
</script>

<style>
*, ::before, ::after {
  box-sizing: border-box;
  padding: 0;
  border: 0;
  margin: 0;
}

#app {
  max-width: 630px;
  padding: 0 15px;
  margin: 0 auto;
  font-family: 'Roboto', sans-serif;
  margin-top: 50px;
  padding-bottom: 100px;
}

input, button {
  font: inherit;
  outline: none;
}

button {
  background: transparent;
}

ul {
  list-style: none;
}

.input {
  display: block;
  width: 100%;
  border: 1px solid #dadce0;
  border-radius: 48px;
  padding: 18px 20px;
  font-size: 20px;
  color: rgb(60, 64, 67);
}

.input:hover {
  border-color: #202124;
}

.input:focus {
  border-color: #1a73e8;
}

footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  left: 0;
  display: flex;
  justify-content: center;
  background: #fff;
}
</style>