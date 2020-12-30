<template>
  <MyToDoList />
  <hr>
  <ParentCounter />
</template>

<script>
import MyToDoList from './components/MyToDoList.vue'
import ParentCounter from "./components/ParentCounter.vue";
export default {
  name: 'App',
  components: {
    ParentCounter,
    MyToDoList
  }
}
</script>
