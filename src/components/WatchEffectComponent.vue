<template>
    <h1>Watch & WatchEffect Component</h1>
    <p>Cek console</p>
    <p>Count: {{ counter }}</p>
    <button class="btn btn-info" @click="add">Add</button>

    <hr>
</template>

<script>
import { ref, reactive, watch, watchEffect, toRefs } from 'vue'
export default {
    setup() {
        const data = reactive({
            counter: 0
        })

        const num1 = ref(1)
        const num2 = ref(2)

        const add = () => {
            num1.value++
            num2.value++
            data.counter++
        }

        watch([num1, num2], (current, before) => {
            console.log('------Ini Watch dengan banyak state------')
            console.log(before)
            console.log(current)
        })

        watch(() => data.counter, (current, before) => {
            console.log('------Ini Watch------')
            console.log(data.counter)
            console.log(`before: ${before}`)
            console.log(`current: ${current}`)
        })

        watchEffect(() => {
            console.log('------Ini WatchEffect------')
            console.log(data.counter)
        }, {
            onTrigger(e) {
                console.log('OnTrigger watchEffect:');
                console.log(e)
            }
        })

        return {
            ...toRefs(data),
            add
        }
    },
}
</script>