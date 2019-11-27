<template>
    <div>
        <h3>Todo</h3>

        <template v-if="notCompletedTodos">
            <ul id="incomplete-tasks">
                <li v-for="todo in notCompletedTodos" :key="todo.id">
                    <label>{{todo.name}}</label>
                    <button class="complete" @click="completeTodo(todo.id)">Complete</button>
                    <button class="delete">Delete</button>
                </li>
            </ul>
        </template>

        <template v-else>
            <ul>
                <li>No todo now</li>
            </ul>
        </template>
    </div>
</template>

<script>
    export default {
        name: "ToDoList",
        props: {
            notCompletedTodos: {
                type: Array,
                require: true
            },
        },
        methods: {
            completeTodo(todoId) {
                let currentTodo = this.notCompletedTodos.find(x => x.id === todoId);

                this.$emit('complete-todo', currentTodo);
            }
        },
    }
</script>

<style scoped>
    li {
        overflow: hidden;
        padding: 20px 0;
        border-bottom: 1px solid #eee;
    }
    li > label {
        font-size: 18px;
        line-height: 40px;
        width: 237px;
        padding: 0 0 0 11px;
    }

    button {
        margin: 0 0 0 10px;
    }
</style>