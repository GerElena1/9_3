<template>
    <div class="wrapper-todo">
        <div class="title has-text-centered">My Todo</div>
        <form @submit.prevent="addTodo">
            <div class="field is-grouped mb-5">
                <p class="control is-expanded">
                    <input v-model="newTodoContent" class="input" type="text" placeholder="Add todo">
                </p>
                <p class="control">
                    <button :disabled="!newTodoContent" class="button is-info">
                        Add
                    </button>
                </p>
            </div>
        </form>

        <div v-for="todo in todos" :key="todo.id" class="card" :class="{ 'has-background-success-light': todo.done }">
            <div class="card-content">
                <div class="content">
                    <div class="columns is-vcentred">
                        <div class="column" :class="{ 'has-text-success line-through': todo.done }">{{ todo.content }}
                        </div>
                        <div class="column has-text-right">
                            <button @click="toggleDone(todo.id)" class="button is-lite"
                                :class="todo.done ? 'is-success' : 'is-ligth'">&check;</button>
                            <button @click="deleteTodo(todo.id)" class="button is-danger ml-2">&cross;</button>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
//импорт
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";
//Todo
const todos = ref([
    // { id: 'id1', content: 'Text 1', done: false },
    // { id: 'id2', content: 'Text 2', done: true }
]);

//методы
const newTodoContent = ref("");
//добавление
const addTodo = () => {
    const newTodo = { id: uuidv4(), content: newTodoContent.value, done: false }
    todos.value.unshift(newTodo)
    newTodoContent.value = ""
}
//удаление
const deleteTodo = id => {
    todos.value = todos.value.filter((todo) => todo.id !== id)
}
//признак выполнения
const toggleDone = id => {
    const index = todos.value.findIndex(todo => todo.id === id)
    todos.value[index].done = !todos.value[index].done
}
</script>

<style>
@import 'node_modules\bulma\css\bulma.min.css';

.wrapper-todo {
    margin: 0 auto;
    max-width: 400px;
    padding: 20px;
}

.line-through {
    text-decoration: line-through;
}
</style>