<template>
    <div class="todo-item" v-bind:class="{'is-compelete':todo.completed}">
        <p><input class="item-check" type="checkbox" v-on:change="markComplete">{{todo.title}}</p>
        <a class="delete" @click="$emit('delete-todo', todo.id)">
            <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
        </a>
        <a class="edit">
            <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
        </a>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ["todo"],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style lang="sass" scoped>

@import "./../sass/variables"

.todo-item
    display: flex
    flex-direction: row
    align-items: center
    border-top: 2px solid $border-color
    p
        flex: 2
        margin: 24px auto
        display: flex
        flex-direction: row
        align-items: center
input.item-check
    -webkit-appearance: none
    padding: 6px
    border: 2px solid $primary-color
    margin-left: 16px
    border-radius: 6px
    position: relative
    &:hover
        cursor: pointer
    &:checked
        background-color: $primary-color
        color: white
    &:checked:after
        content: '\2714'
        font-size: 14px
        position: absolute
        top: -5px
        left: 1px
        color: white
.delete, .edit
    margin-left: 24px
.delete .icon:hover
    cursor: pointer
    stroke: $delete-color

.edit .icon:hover
    cursor: pointer
    stroke: $edit-color

.icon
	width: 24px
	height: 24px
	stroke: $dark3-color


</style>