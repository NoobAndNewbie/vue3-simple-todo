<template>
    <h1>Reactive Component</h1>
    <p>Nama: {{ name }}</p>
    <p>Umur: {{ age }}</p>

    <hr>
</template>

<script>
import { reactive, toRefs } from 'vue'
export default {
    setup() {
        const data = reactive({
            name: 'Candra',
            age: 24
        })

        setTimeout(() => {
            data.name += ' Darmawan'
            data.age = 25
        }, 1000)

        return {
            ...toRefs(data)
        }
    },
}
</script>