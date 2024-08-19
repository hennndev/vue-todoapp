<script>
    import Todo from './Todo.vue';
    export default {
        data() {
            return {
                isChecked: false
            }
        },
        props: ['todos', 'editTodo', 'deleteTodo', 'handleCheckedAll', 'clearTodos', 'handleIsEdit', 'handleTodoEdit'],
        components: {
            Todo
        }, 
        methods: {
            handleChecked(e) {
                this.handleCheckedAll(e.target.checked)
            },
            handleClearTodos() {
                if(this.isChecked) {
                    this.clearTodos()
                    this.isChecked = false
                }
            }
        }
    }
</script>

<template>
    <section class="todos">
        <article class="flex-between todos-header">
            <h1>My Todos</h1>
            <p>{{ new Date().toDateString() }}</p>
        </article>
        <section class="todo-container">
            <template v-for="todo in this.todos" :key="todo.id">
                <Todo 
                    :todo="todo" 
                    :editTodo="this.editTodo" 
                    :deleteTodo="this.deleteTodo"
                    :handleIsEdit="this.handleIsEdit"
                    :handleTodoEdit="this.handleTodoEdit"/>
            </template>

            <p v-show="this.todos.length < 1" class="todos-empty">
                You have no todos yet
            </p>
        </section>

        <section class="flex-end todos-bottom" v-show="todos.length > 0">
            <label class="custom-checkbox">
                <input type="checkbox" v-model="this.isChecked" @change="handleChecked">
                <span class="checkmark"></span>
            </label>
            <button class="btn-clear"  @click="handleClearTodos" :class="!this.isChecked ? 'btn-disabled' : ''" :disabled="!this.isChecked">Clear All</button>
        </section>
    </section>
</template>

<style>
    .todos {
        padding: 20px;
        border-radius: 10px;
        background-color: var(--primary);
    }
    .todos-header {
        margin-bottom: 20px;
        border-bottom: 1px solid #ccc;
        padding-bottom: 20px;
    }
    .todos-header h1 {
        font-size: 25px;
        color: var(--secondary);
        font-weight: bold;
    }
    .todos-header p {
        color: gray;
    }

    .todo-container {
        flex-direction: column;
    }
    .todos-empty {
        color: gray;
    }       



    .custom-checkbox input[type="checkbox"] {
        display: none;
    }

    /* Create a custom checkbox */
    .custom-checkbox {
        display: inline-block;
        cursor: pointer;
        user-select: none;
        font-size: 18px;
    }

/* The "box" of the custom checkbox */
    .custom-checkbox .checkmark {
        display: inline-block;
        width: 20px;
        height: 20px;
        background-color: #f1f1f1;
        border: 2px solid #ccc;
        border-radius: 4px;
        vertical-align: middle;
        margin-right: 10px;
        position: relative;
    }

    /* The checkmark (tick) */
    .custom-checkbox input[type="checkbox"]:checked + .checkmark::after {
        content: "";
        position: absolute;
        left: 6.5px;
        top: 2px;
        width: 5px;
        height: 10px;
        border: solid white;
        border-width: 0 3px 3px 0;
        transform: rotate(45deg);
    }

    /* When the checkbox is checked, change the background */
    .custom-checkbox input[type="checkbox"]:checked + .checkmark {
        background-color: var(--secondary);
        border-color: var(--secondary);
    }


    .todos-bottom {
        margin-top: 40px;
        border-top: 1px solid #ccc;
        padding-top: 10px;
        column-gap: 5px;
    }


    .btn-clear {
        border: none;
        outline: none;
        border-radius: 8px;
        padding: 10px 12px;
        font-size: medium;
        background: var(--secondary);
        color: white;
        cursor: pointer;
    }
    .btn-disabled {
        background: gray;
        cursor: not-allowed;
    }
</style>