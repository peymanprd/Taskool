<template>
  <div id="app">
    <div class="container">
        <div id="nav">
            <router-link to="/"><img src="./assets/logo.svg" alt="taskool logo"></router-link>
        </div>
        <CreateTodo v-on:create-todo="createTodo" />
        <span class="queue-title"><svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01"></path></svg>لیست وظایف فعال</span>
        <Todos v-bind:todos="todos" v-on:edit-todo="editTodo" v-on:update-todo="updateTodo" v-on:delete-todo="deleteTodo" />
        <!-- <Todos v-bind:todos="todos" /> -->
    </div>
    <router-view/>
  </div>
</template>

<script>

import CreateTodo from "./components/CreateTodo"
import Todos from "./components/Todos"

export default {
    components: {
        CreateTodo,
        Todos
    },
    methods: {
      deleteTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      editTodo(index) {
          for(var i = this.todos.length - 1; i >= 0; i--) {
              this.todos[i].edit = false
          }
          this.todos[index].edit = !this.todos[index].edit
      },
      updateTodo(title, index) {
        console.log(title)
        this.todos[index].title = title
        this.todos[index].edit = false
      },
      createTodo(newTodo) {
          (newTodo.title.length !== 0) ? this.todos = [...this.todos, newTodo] : console.log('Not given')
      }
    },
    data() {
        return {
            todos: [
                {
                    id: 1,
                    title: "نسخه آزمایشی وظیفه شماره یک",
                    edit: false,
                    done: false
                },
                {
                    id: 2,
                    title: "نمونه آزمایشی شماره دو",
                    edit: false,
                    done: false
                },
                {
                    id: 3,
                    title: "نمونه آزمایشی وظیفه نهایی",
                    edit: false,
                    done: false
                }
            ]
        }
    }
}
</script>

<style lang="sass">
@import "./sass/variables"

*,*::before,*::after
    box-sizing: border-box
    outline: none
body
    direction: rtl

a
  display: flex
button:hover
    cursor: pointer
#app
  font-family: "Estedad", Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale

.queue-title
  font-size: $font-size
  font-weight: 400
  color: $dark3-color
  display: flex
  align-items: center
  margin-top: 48px
  margin-bottom: 16px
  .icon
    width: 24px
    height: 24px
    stroke: $dark3-color
    margin-left: 8px
  @media screen and (max-width: 768px)
    margin-top: 24px

#nav
    display: flex
    flex-direction: row
    justify-content: space-between
    align-items: center
    margin-top: 48px
.container
    max-width: 730px
    margin: 0 auto
    @media screen and (max-width: 768px)
        max-width: 90%
</style>
