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
            clearTodos() {
                this.todos = []
                this.isEdit = false
                this.todoEdit = null
                localStorage.removeItem('todos')
            },

            handleIsEdit(value) {
                this.isEdit = value
            },
            handleTodoEdit(todo) {
                this.todoEdit = todo
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
                localStorage.setItem('todos', JSON.stringify(updatedTodos))
            }
        }
    }
</script>

<template>
    <main class="main flex-center">
        <section class="todos-container">
            <AddForm 
                :addTodo="addNewTodo" 
                :isEdit="isEdit" 
                :todoEdit="todoEdit" 
                :editTodo="editTodo"
                :handleIsEdit="handleIsEdit"
                :handleTodoEdit="handleTodoEdit"/>
            <Todos 
                :todos="todos" 
                :editTodo="editTodo" 
                :handleIsEdit="handleIsEdit"
                :deleteTodo="deleteTodo"
                :handleTodoEdit="handleTodoEdit"
                :handleCheckedAll="handleCheckedAll"
                :clearTodos="clearTodos"/>
        </section>
    </main>
</template>

<style>
    .main {
        min-height: 100vh;
        background: var(--secondary);
    }
    .todos-container {
        width: 450px;
        min-height: 400px;
    }
</style>