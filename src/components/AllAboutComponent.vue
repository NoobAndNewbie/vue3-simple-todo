<template>
    <h1>All about component</h1>
    <h3>{{ label.toUpperCase() }}</h3>
    <p>Nama: {{ nameCombine }}</p>
    <p>Umur: {{ user.age }}</p>

    <button class="btn btn-primary" @click="submit">Submit</button>

    <slot />
</template>

<script>
import { computed, toRefs, onMounted } from 'vue'

export default {
    props: {
        label: {
            type: String,
            default: ''
        },
        user: {
            type: Object,
            default: () => {}
        }
    },
    setup(props, { attrs, slots, emit }) {
        const { label, user } = toRefs(props)
        const nameCombine = computed(() => `${user.value.name} Mamamia`)

        onMounted(() => {
            console.log(attrs)
            console.log(slots)
        })

        const submit = () => {
            emit('submit', 'Ini adalah pesan dari child component')
        }

        return { nameCombine, submit }
    },
}
</script>