<template>
  <li class="todo-item"
    v-bind:class="{'done': done}"
    v-on:click="handleClick">
    <span v-if="done">✓</span>
<!--      {{ text }}-->
    <slot />
  </li>
</template>

<script>
export default {
  name: "MyToDoItem",
  props: {
    // text: {
    //   type: String
    // },
    done: {
      type: Boolean
    }
  },
  emits: ['toggle'],
  methods: {
    handleClick() {
      console.log('handle click!!!')
      this.$emit('toggle')
    }
  }
}
</script>

<style scoped>

</style>
