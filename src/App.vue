<script>
    import AddForm from './components/AddForm.vue';
    import Todos from './components/Todos.vue';

    export default {
        data() {
            return {
                todos: [],
                todoEdit: null,
                isEdit: false
            }
        },
        components: {
            AddForm,
            Todos
        },
        created() {
            console.log('Mounted')
            const todosData = JSON.parse(localStorage.getItem('todos'))
            if(todosData || todosData?.length > 0) {
                this.todos = todosData
            }
        },
        methods: {
            // todos
            addNewTodo(value) {
                const newTodo = {
                    id: new Date().getTime(),
                    text: value,
                    isDone: false
                }
                this.todos.push(newTodo)
                localStorage.setItem('todos', JSON.stringify(this.todos))
            },
            editTodo(id, newData) {
                const updatedTodos = this.todos.map(todo => {
                    if(todo.id === id) {
                        return {
                            ...todo,
                            ...newData
                        }
                    } else {
                        return todo
                    }
                })
                this.todos = updatedTodos
                localStorage.setItem('todos', JSON.stringify(updatedTodos))
            },
            deleteTodo(id) {
                const confirm = window.confirm("Are you sure want to delete this todo?")
                if(confirm) {
                    const updatedTodos = this.todos.filter(todo => todo.id !== id)
                    this.todos = updatedTodos
                    localStorage.setItem('todos', JSON.stringify(updatedTodos))
                }
            },
            handleCheckedAll(value) {
                const updatedTodos = this.todos.map(todo => {
                    if(value === true) {
                        return {
                            ...todo,
                            isDone: true
                        }
                    } else {
                        return {
                            ...todo,
                            isDone: false
                        }
                    }
                })
                this.todos = updatedTodos
            },
            clearTodos() {
                const confirm = window.confirm('Are you sure want to clear todos?')
                if(confirm) {
                    this.todos = []
                    this.isEdit = false
                    this.todoEdit = null
                    localStorage.removeItem('todos')
                }
            },
            // isEdit
            handleIsEdit(value) {
                this.isEdit = value
            },
            // todoEdit
            handleTodoEdit(todo) {
                this.todoEdit = todo
            },

        }
    }
</script>

<template>
    <main class="main flex-center">
        <section class="todos-container">
            <AddForm 
                :addTodo="addNewTodo" 
                :editTodo="editTodo"
                :isEdit="isEdit" 
                :handleIsEdit="handleIsEdit"
                :todoEdit="todoEdit" 
                :handleTodoEdit="handleTodoEdit"/>
            <Todos 
                :todos="todos" 
                :editTodo="editTodo" 
                :deleteTodo="deleteTodo"
                :clearTodos="clearTodos"
                :handleCheckedAll="handleCheckedAll"
                :handleIsEdit="handleIsEdit"
                :handleTodoEdit="handleTodoEdit"/>
        </section>
    </main>
</template>

<style>
    .main {
        min-height: 100vh;
        background: var(--secondary);
        padding: 0 20px;
    }
    .todos-container {
        width: 450px;
        min-height: 400px;
        margin: 20px 0;
    }
</style>