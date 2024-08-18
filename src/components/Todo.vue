<script>
    export default {
        props: ['todo', 'editTodo', 'deleteTodo', 'handleIsEdit', 'handleTodoEdit'],
        methods: {
            handleEdit(e) {
                this.handleIsEdit(true)
                this.handleTodoEdit(this.todo)
            },
            handleChecked(e) {
                const updatedTodo = {
                    ...this.todo,
                    isDone: e.target.checked
                }
                this.editTodo(this.todo.id, updatedTodo)
            },
            handleDelete() {
                this.deleteTodo(this.todo.id)
            }
        }
    }
</script>

<template>
    <article class="todo flex-between">
        <div class="flexx todo-value">
            <label class="custom-checkbox">
                <input type="checkbox" :checked="this.todo.isDone" @change="handleChecked">
                <span class="checkmark"></span>
            </label>
            <p :class="this.todo.isDone ? 'todo-done' : ''">{{ this.todo.text }}</p>
        </div>
        <div class="flexx todo-icons">
            <i class="pi pi-pencil edit-icon" @click="handleEdit" :class="this.todo.isDone ? 'edit-icon-hidden' : ''"></i>
            <i class="pi pi-trash delete-icon" @click="handleDelete"></i>
        </div>
    </article>
</template>

<style>
    .todo {
        cursor: pointer;
        margin-bottom: 30px;
    }
    .todo-value input {
        margin-right: 10px;
        color: gray;
    }
    .todo-value p {
        font-size: large;
        color: gray;
    }
    .todo:hover p {
        text-decoration: line-through
    }
    .todo .delete-icon {
        display: none;
        font-size: 1.4 rem;
        color: var(--secondary);
        cursor: pointer;
    }
    .todo:hover .delete-icon {
        display: block
    }

    .todo-done {
        text-decoration: line-through;
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



    .todo-icons {
        column-gap: 1.2rem;
    }
    .todo .edit-icon {
        display: none;
        font-size: 1.4 rem;
        color: var(--secondary);
        cursor: pointer;
    }
    .todo:hover .edit-icon {
        display: block
    }
    .todo .edit-icon-hidden {
        display: none !important;
    }
</style>