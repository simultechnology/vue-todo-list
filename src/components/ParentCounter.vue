<template>
  <SwitchButton />
  <SimpleCounter
    v-bind:count="myCount"
    v-on:update="handleUpdate">
    <template v-slot:default="{ foo }">
      <p> {{ foo }} </p>
    </template>
  </SimpleCounter>
</template>
<script>
import SimpleCounter from "./SimpleCounter.vue";
import SwitchButton from "./SwitchButton.vue";
export default {
  name: "ParentCounter",
  components: {SwitchButton, SimpleCounter },
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
