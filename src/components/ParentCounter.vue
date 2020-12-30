<template>
  <SimpleCounter
    v-bind:count="myCount"
    v-on:update="handleUpdate" />
</template>
<script>
import SimpleCounter from "./SimpleCounter.vue";
export default {
  name: "ParentCounter",
  components: { SimpleCounter },
  data() { return { myCount: 0 } },
  methods: {
    handleUpdate(newCount) {
      this.myCount = newCount
    }
  }
}
</script>

<style scoped>

</style>
