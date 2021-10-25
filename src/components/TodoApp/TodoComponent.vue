<template>
    <h1>Todo App</h1>

    <div class="card mt-3 mb-5">
        <div class="card-body">
            <div class="card-title">Simple Todo App</div>
            <div class="row">
                <div class="col-10">
                    <input v-model="todo" type="text" class="form-control" @keyup.enter="add">
                </div>
                <div class="col-2">
                    <button class="btn btn-primary" @click="add">Add</button>
                </div>
            </div>
            <small>Total Todo: {{ totalTodo }}</small>

            <list-component :todos="list" @doneTodo='doneTodo' @deleteTodo='deleteTodo' />
        </div>
    </div>
</template>

<script>
import { ref, reactive, onMounted, computed, toRefs } from 'vue'
import ListComponent from './ListComponent.vue'

export default {
  components: { ListComponent },
    setup() {
        const todo = ref('')
        const todos = reactive({
            list: []
        })

        onMounted(() => {
            const items = localStorage.getItem('todos')
            todos.list = items ? JSON.parse(items) : []
        })

        const totalTodo = computed(() => todos.list.length)
        const add = () => {
            todos.list.unshift({
                activity: todo.value,
                isDone: false
            })
            todo.value = ''
            saveToLocalStorage()
        }

        const doneTodo = todoIndex => {
            todos.list = todos.list.filter((item, index) => {
                if(index === todoIndex)
                    item.isDone = true

                return item
            })
            saveToLocalStorage()
        }
        
        const deleteTodo = todoIndex => {
            todos.list = todos.list.filter((item, index) => {
                if(index !== todoIndex) 
                    return item
            })
            saveToLocalStorage()
        }

        const saveToLocalStorage = () => {
            localStorage.setItem('todos', JSON.stringify(todos.list))
        }

        return {
            todo,
            ...toRefs(todos),
            totalTodo,
            add,
            doneTodo,
            deleteTodo
        }
    }
}
</script>