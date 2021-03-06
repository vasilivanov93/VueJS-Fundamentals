<template>
    <div class="container">
        <button @click="changeTab('AddToDo')">Add</button>
        <button @click="changeTab('ToDoList')">ToDo</button>
        <button @click="changeTab('CompletedToDo')">Complete</button>

        <keep-alive>
            <component :is="activeTab"
                       :notCompletedTodos="notCompletedTodos"
                       :completedTodos="completedTodos"
                       @add-todo="onAddTodo"
                       @complete-todo="onCompleteTodo"
                       @restore-todo="onRestoreTodo"
                       @remove-todo="onRemoveTodo"
            >
            </component>
        </keep-alive>
    </div>
</template>

<script>
    // Components
    import AddToDo from "./components/AddToDo";
    import ToDoList from "./components/ToDoList";
    import CompletedToDo from "./components/CompletedToDo";

    // Data
    import {todos} from "./data/todos";

    export default {
        name: 'app',
        components: {CompletedToDo, ToDoList, AddToDo},
        comments: {
            AddToDo,
            ToDoList,
            CompletedToDo
        },
        data() {
            return {
                activeTab: 'AddToDo',
                todos,
                idTodo: todos.length
            }
        },
        computed: {
            notCompletedTodos() {
                return this.todos.filter(x => !x.isCompleted);
            },
            completedTodos() {
                return this.todos.filter(x => x.isCompleted)
            }
        },
        methods: {
            changeTab(tabName) {
                this.activeTab = tabName
            },
            onAddTodo(todoName) {
                this.todos.push({
                    id: this.idTodo++,
                    name: todoName,
                    isCompleted: false,
                    isEdit: false
                });
            },
            onCompleteTodo(todo) {
                todo.isCompleted = true;
            },
            onRestoreTodo(todo) {
                todo.isCompleted = false;
            },
            onRemoveTodo(todo) {
                this.todos = this.todos.filter(x => x.id !== todo.id);
            }
        },
    }
</script>

<style>
    body {
        background: #fff;
        color: #333;
        font-family: Lato, sans-serif;
    }

    .container {
        display: block;
        width: 400px;
        margin: 100px auto 0;
    }

    ul {
        margin: 0;
        padding: 0;
    }

    li * {
        float: left;
    }

    li,
    h3 {
        clear: both;
        list-style: none;
    }

    input,
    button {
        outline: none;
    }

    button {
        background: none;
        border: 0px;
        color: #888;
        font-size: 15px;
        width: 60px;
        margin: 10px 0 0;
        font-family: Lato, sans-serif;
        cursor: pointer;
    }

    button:hover {
        color: #333;
    }

    h3,
    label[for="new-task"] {
        color: #333;
        font-weight: 700;
        font-size: 15px;
        border-bottom: 2px solid #333;
        padding: 30px 0 10px;
        margin: 0;
        text-transform: uppercase;
    }

    input[type="text"] {
        margin: 0;
        font-size: 18px;
        line-height: 18px;
        height: 18px;
        padding: 10px;
        border: 1px solid #ddd;
        background: #fff;
        border-radius: 6px;
        font-family: Lato, sans-serif;
        color: #888;
    }

    input[type="text"]:focus {
        color: #333;
    }
</style>
