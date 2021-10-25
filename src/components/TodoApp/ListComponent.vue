<template>
    <div class="mt-4">
        <ul class="list-group">
            <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
                <div class="row">
                    <div class="col my-auto">
                        <span v-if="todo.isDone">
                            <del>{{ index+1 }}. {{ todo.activity }}</del>
                        </span>
                        <span v-else>{{ index+1 }}. {{ todo.activity }}</span>
                    </div>
                    <div class="col-auto">
                        <button class="btn btn-success me-2" @click="doneTodo(index)">Done</button>
                        <button class="btn btn-danger" @click="deleteTodo(index)">Delete</button>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        todos: {
            type: Array,
            default: []
        }
    },
    setup(_, { emit }) {
        const doneTodo = index => {
            emit('doneTodo', index)
        }

        const deleteTodo = index => {
            emit('deleteTodo', index)
        }

        return { doneTodo, deleteTodo }
    }
}
</script>