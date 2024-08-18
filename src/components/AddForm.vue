<template>
    <form class="form" @submit="submitTodo">
        <input type="text" v-model="todo" placeholder="Create new todo...">
        <i v-show="!this.isEdit" class="pi pi-plus add-icon" @click="submitTodo"></i>
        <i v-show="this.isEdit" class="pi pi-pencil add-icon" @click="submitTodo"></i>
        <i class="pi pi-times close-icon"></i>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                todo: ''
            }
        },
        props: ['addTodo', 'isEdit', 'todoEdit', 'editTodo'],
        methods: {
            submitTodo() {
                if(this.todo === '') {
                    return alert('Please fill your todo input')
                } else {
                    this.addTodo(this.todo)
                }
            },
        }
    }
</script>

<style>

    .form {
        display: flex;
        align-items: center;
        width: 100%;
        background: var(--primary);
        border-radius: 10px;
        padding: 0 20px;
        margin-bottom: 20px;
    }
    .form input {
        flex: 1;
        border: none;
        outline: none;
        font-size: large;
        margin-right: 10px;
        padding: 16px 0;
        background-color: transparent;
        color: gray;
    }
    .form .add-icon {
        font-size: 1.1rem;
        color: var(--secondary);
        cursor: pointer;
    }
    .form .close-icon {
        font-size: 0.8rem;
        color: gray;
        cursor: pointer;
        margin-left: 20px;
    }

</style>