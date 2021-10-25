<template>
    <h1>Methods & Computed Component</h1>
    <p>Count: {{ counter }} | Total Number: {{ countTotal }}</p>
    <button class="btn btn-primary" @click="add">Add</button>

    <hr>
</template>

<script>
import { computed, reactive, ref, toRefs } from 'vue'
export default {
    setup() {
        const data = reactive({
            counter: 0
        })

        const addNum = ref(1)

        const add = () => {
            countTotal.value = 5
            data.counter++
        }

        // Computed tanpa getter & setter
        // const countTotal = computed(() => data.counter + addNum.value)

        const countTotal = computed({
            get: () => data.counter + addNum.value,
            set: val => addNum.value = val
        })

        return {
            ...toRefs(data),
            add,
            countTotal
        }
    },
}
</script>