<template>
  <h1>Ini ref component</h1>
  <h3>{{ message }}</h3>

  <hr>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    const message = ref('Coba refresh')

    setTimeout(() => {
      message.value = 'Mamamia'
    }, 2000)

    return {
      message
    }
  },
}
</script>
