<template>
    <div>
        <h3>Completed</h3>

        <ul id="completed-tasks">
            <li v-for="todo in completedTodos" :key="todo.id">
                <label>{{todo.name}}</label>
                <button class="restore" @click="restoreTodo(todo.id)">Restore</button>
                <button class="delete" @click="removeTodo(todo.id)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "CompletedToDo",
        props: {
            completedTodos: {
                type: Array,
                require: true
            }
        },
        methods: {
            restoreTodo(todoId) {
                let currentTodo = this.completedTodos.find(x => x.id === todoId);

                this.$emit('restore-todo', currentTodo);
            },
            removeTodo(todoId) {
                let currentTodo = this.completedTodos.find(x => x.id === todoId);

                this.$emit('remove-todo', currentTodo);
            }
        },
    }
</script>

<style scoped>
    #completed-tasks label {
        text-decoration: line-through;
        color: #888;
    }

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

    li > .delete:hover {
        color: #cf2323;
    }
</style>