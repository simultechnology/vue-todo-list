<template>
  <dialog>
    <h1>
      <slot name="title" />
    </h1>
    <div>
      <slot />
    </div>
  </dialog>
</template>

<script>
export default {
name: "ModalDialog"
}
</script>

<style scoped>

</style>
