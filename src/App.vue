<template>
  <!-- Ini ref component - Hanya berlaku untuk tipe data primitif -->
  <ref-component />

  <!-- Ini reactive component -->
  <reactive-component />

  <!-- Ini methods & Computed component -->
  <methods-component />

  <!-- Ini watchEffect component -->
  <watch-effect-component />

  <!-- Ini yang berkaitan dengan component (props, emit, dll) -->
  <all-about-component :label="label" :user="user" yolo="active" @submit="onSubmit">
    <p>Ini adalah slot</p>
  </all-about-component>
  <button class="btn btn-outline-primary" @click="changeName">Change Name</button><hr>

  <!-- Ini adalah simple project todo -->
  <todo-component />
</template>

<script>
import RefComponent from './components/RefComponent.vue'
import ReactiveComponent from './components/ReactiveComponent.vue'
import MethodsComponent from './components/MethodsComponent.vue'
import WatchEffectComponent from './components/WatchEffectComponent.vue'
import AllAboutComponent from './components/AllAboutComponent.vue'
import TodoComponent from './components/TodoApp/TodoComponent.vue'

// Ini adalah life cycle di vue 3
// import {
//     onBeforeMount,
//     onMounted,
//     onBeforeUpdate,
//     onUpdated,
//     onBeforeUnmount,
//     onUnmounted,
//     onActivated,
//     onDeactivated,
//     onErrorCaptured
// } from 'vue'

import { ref, reactive } from 'vue'

export default {
  components: { 
    RefComponent,
    ReactiveComponent,
    MethodsComponent,
    WatchEffectComponent,
    AllAboutComponent,
    TodoComponent
  },
  setup() {
    const label = ref('biodata')
    const user = reactive({
      name: 'Candra Darmawan',
      age: 24
    })

    const changeName = () => {
      user.name = 'Stephen Chow'
    }

    const onSubmit = val => {
      alert(val)
    }

    return {
      label,
      user,
      changeName,
      onSubmit
    }
  }
}
</script>
