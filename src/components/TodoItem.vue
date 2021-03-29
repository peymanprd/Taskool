<template>
    <div class="todo-item" v-bind:class="{'is-done':todo.done}">
        <div class="edit-item" v-if="todo.edit">
            <input @keyup.enter="$emit('update-todo')" type="text" v-model="todo.title" ref="title">
            <!-- <button class="clear" @click="clearTodo(todo.title)">
                <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12"></path></svg>
            </button> -->
            <div class="actions">
                <button class="confirm" @click="$emit('update-todo')">ویرایش</button>
                <button class="cancel" @click="cancelEdit()">انصراف</button>
            </div>
        </div>
        <div class="check-item" v-else><input class="item-check" type="checkbox" v-on:change="markDone">{{todo.title}}</div>
        <div class="option-item" v-if="!todo.edit & !todo.done">
            <a class="edit" @click="$emit('edit-todo')">
                <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
            </a>
            <a class="delete" @click="$emit('delete-todo', todo.id)">
                <svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
            </a>
        </div>
    </div>

</template>

<script>
export default {
    name: 'TodoItem',
    props: ["todo"],
    methods: {
        cancelEdit() {
            this.todo.title
            this.todo.edit = !this.todo.edit
        },
        markDone() {
            this.todo.done = !this.todo.done
        }
        // clearTodo(title) {
        //     (this.todo.title.length) ? this.todo.title = '' : this.todo.title = title
        // }
    }
}
</script>

<style lang="sass" scoped>

@import "./../sass/variables"

.is-done
    -webkit-text-decoration-line: line-through
    text-decoration-line: line-through
    color: $dark4-color

.todo-item
    display: flex
    flex-direction: row
    align-items: center
    border-top: 2px solid $border-color
    width: 100%
    .check-item
        width: 100%
        height: 40px
        margin: 24px auto
        display: flex
        flex-direction: row
        align-items: center
        @media screen and (max-width: 768px)
            height: auto
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
        top: -6px
        left: 2px
        color: white
.option-item 
    display: flex
    flex-direction: row
    justify-content: flex-end
.edit,.delete
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
	stroke: $dark2-color

.edit-item
    display: flex
    flex-direction: row
    align-items: center
    width: 100%
    padding: 24px auto
    @media screen and (max-width: 768px)
        flex-direction: column
        flex-wrap: wrap
    input
        position: relative
        border: 2px solid lighten($dark2-color, 11%)
        padding: 6.5px 12px
        border-radius: 6px
        flex: 4
        margin: 24px auto
        font-family: "Estedad"
        font-size: $font-size - 2
        margin-left: 16px
        @media screen and (max-width: 768px)
            width: 100%
            margin-top: 16px
            margin-bottom: 0
            margin-left: 0
        &:hover, &:focus
            border-color: $primary-color
    .clear
        position: relative
        left: 6%
        border: 0
        border-radius: 99px
        background-color: $border-color
        display: flex
        justify-content: center
        align-items: center
        width: 28px
        height: 24px
        &:hover
            background-color: $dark2-color
            .icon
                stroke: $dark6-color
        .icon
            width: 12px
            height: 12px
            stroke: $dark4-color
    .actions
        margin: 0
        display: flex
        flex-direction: row
        margin: 24px auto
        flex: 1
        @media screen and (max-width: 768px)
            width: 50%
            margin: 16px auto
            margin-left: 0
            margin-right: auto
        button
            background-color: $border-color
            color: dark5-color
            border: 0
            font-family: "Estedad"
            font-size: $font-size - 2
            font-weight: 400
            width: 80px
            height: 40px
            border-radius: 6px
            &:first-child
                margin-left: 8px
                background-color: $edit-color
                color: $snow
                &:hover
                    background-color: lighten($edit-color, 5%)
            &:last-child:hover
                color: $primary-color
            @media screen and (max-width: 768px)
                display: block
                width: 100%

</style>