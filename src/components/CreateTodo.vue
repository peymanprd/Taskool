<template>
    <form @submit="createTodo">
        <input class="title-todo" type="text" v-model="title" placeholder="یک وظیفه تعریف کنید">
        <button class="create-todo"><svg class="icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path></svg></button>
    </form>
</template>

<script>

import uuid from "uuid";

export default {

    name: "CreateTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        createTodo(e) {
            e.preventDefault();
            const newTodo = {
                id: uuid.v4(),
                title: this.title,
                done: false
            }
            this.$emit('create-todo', newTodo);
            this.title = '';
        }
    }

}

</script>

<style lang="sass" scoped>
@import "./../sass/variables"
form
    margin-top: 96px
    width: 100%
    border: 0
    background-color: $border-color
    border-radius: 12px
    display: flex
    flex-direction: row
    align-items: center
    padding-right: 24px
    padding-left: 10px
@media screen and (max-width: 768px)
	form
		margin-top: 56px
.title-todo
    background: none
    border: 0
    padding: 16.5px 0
    border-radius: 12px
    width: 90%
    font-family: "Estedad"
    font-size: $font-size
::-webkit-input-placeholder
    color: $dark3-color
    font-size: $font-size - 2

.create-todo
    border: 0
    background-color: white
    color: $primary-color
    height: 32px
    width: 32px
    margin-right: auto
    margin-left: 10px
    border-radius: 999px
    display: flex
    justify-content: center
    align-items: center
    box-shadow: 0 5px 10px 0 rgba($dark5-color, .1)
    &:hover
        cursor: pointer
        color: white
        background-color: $primary-color
        .icon
            stroke: white

.icon
	width: 24px
	height: 24px
	stroke: $primary-color
</style>