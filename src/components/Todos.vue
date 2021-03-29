<template>
    <div>
        <div v-bind:key="todo.id" v-for="(todo,index) in todos">
            <TodoItem v-bind:todo="todo" v-on:edit-todo="$emit('edit-todo', index)" v-on:update-todo="$emit('update-todo', todo.title, index)" v-on:delete-todo="$emit('delete-todo', todo.id)" />
        </div>
    </div>
</template>

<script>

import TodoItem from './TodoItem.vue'

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"]
}

</script>