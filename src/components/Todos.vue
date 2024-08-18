<template>
    <section class="todos">
        <article class="flex-between todos-header">
            <h1>My Todos</h1>
            <p>{{ new Date().toDateString() }}</p>
        </article>
        <section class="todo-container">
            <template v-for="todo in this.todos" :key="todo.id">
                <Todo :todo="todo" :editTodo="this.editTodo" :deleteTodo="this.deleteTodo"/>
            </template>

            <p v-show="this.todos.length < 1" class="todos-empty">
                You have no todos yet
            </p>
        </section>
    </section>
</template>

<script>
    import Todo from './Todo.vue';
    export default {
        props: ['todos', 'editTodo', 'deleteTodo'],
        components: {
            Todo
        }, 
    }
</script>

<style>
    .todos {
        padding: 20px;
        width: 100%;
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
</style>