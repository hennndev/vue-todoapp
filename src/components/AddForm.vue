<script>
    export default {
        data() {
            return {
                todo: ''
            }
        },
        props: ['addTodo', 'editTodo', 'isEdit', 'handleIsEdit', 'todoEdit', 'handleTodoEdit'],
        watch: {
            isEdit() {
                if(this.isEdit) {
                    this.todo = this.todoEdit.text
                }
            }
        },
        methods: {
            submitTodo() {
                if(this.todo === '') {
                    return alert('Please fill your todo input')
                } else {
                    if(this.isEdit) {
                        this.editTodo(this.todoEdit.id, {
                            ...this.todoEdit,
                            text: this.todo
                        })
                        this.handleIsEdit(false)
                        this.handleTodoEdit(null)
                        this.todo = ''
                    } else {
                        this.addTodo(this.todo)
                        this.todo = ''
                    }
                }
            },
            handleCloseEdit() {
                this.handleIsEdit(false)
                this.handleTodoEdit(null)
                this.todo = ''
            }
        }
    }
</script>

<template>
    <form class="form" @submit.prevent="submitTodo">
        <input type="text" v-model="todo" :placeholder="this.isEdit ? 'Edit todo...' : 'Create new todo...'">
        <i :class="!this.isEdit ? 'pi pi-plus' : 'pi pi-pencil'" class="form-icon" @click="submitTodo"></i>
        <i class="pi pi-times close-icon" v-show="this.isEdit" @click="this.handleCloseEdit"></i>
    </form>
</template>

<style>
    .form {
        display: flex;
        align-items: center;
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
    .form .form-icon {
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