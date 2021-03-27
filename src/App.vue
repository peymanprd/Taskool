<template>
  <div id="app">
		<div class="container">
			<nav class="nav">
				<a href="/" class="logo"><img alt="Taskom logo" src="./assets/logo.svg"></a>
				<a class="help" href="/about"><svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>راهنما</a>
			</nav>
			<CreateTodo />
			<h2><svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"></path></svg>لیست وظایف</h2>
			<Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
		</div>
  </div>
</template>

<script>

import CreateTodo from './components/CreateTodo.vue'
import Todos from './components/Todos.vue'

export default {
  name: 'App',
  components: {
		CreateTodo,
    Todos
  },
	data() {
		return {
			todos: [
				{
					id: 1,
					title: "وظیفه شماره یک",
					compeleted: false
				},
				{
					id: 2,
					title: "خرید منزل",
					compeleted: true
				},
				{
					id: 3,
					title: "اتمام پروژه سد سازی مغلستان شرقی",
					compeleted: false
				}
			]
		}
	},
	methods: {
		deleteTodo(id) {
			this.todos = this.todos.filter(todo => todo.id !== id);
		}
	}
}
	
</script>

<style lang="sass">

@import "./sass/variables"
@import "./sass/base"

*, *::before, *::after
	box-sizing: border-box
	outline: none
#app
  font-family: "Estedad", Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  margin-top: 48px

h1,h2,h3,h4,h5,h6,p,a,button
	font-size: $font-size
	font-family: "Estedad"

body
	direction: rtl
a
	display: flex
	vertical-align: middle
h2
	display: flex
	flex-direction: row
	align-items: center
	margin-top: 48px
	margin-bottom: 16px
	color: $dark3-color
	font-weight: 400
	font-size: $font-size
	.icon
		width: 20px
		height: 20px
		stroke: $dark2-color
		margin-left: 12px

.container
	max-width: 730px
	margin: 0 auto

@media screen and (max-width: 760px)
	.container
		max-width: 90%

.nav
	display: flex
	flex-direction: row
	justify-content: space-between

.help
	text-decoration: none
	color: $dark5-color
	padding: 10px 20px
	display: flex
	direction: row
	align-items: center
	font-weight: 500
	&:hover
		color: $primary-color
	.icon
		width: 24px
		height: 24px
		stroke: $dark4-color
		margin-left: 4px


</style>
