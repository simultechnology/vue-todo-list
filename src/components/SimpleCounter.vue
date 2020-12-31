<template>
  <h1> Counter </h1>
  <slot v-bind:foo="'Hello World'" />
  カウント: {{ count }}
  <button v-on:click="handleClick">+1</button>
</template>

<script>
export default {
  name: "SimpleCounter",
  props: { count: { type: Number } },
  emits: ['update'],
  methods: {
    handleClick() {
      const newCount = this.count + 1
      this.$emit('update', newCount)
    }
  }
}
</script>

<style scoped>

</style>
