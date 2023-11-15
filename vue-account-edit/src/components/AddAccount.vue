<!-- eslint-disable prettier/prettier -->
<template>
  <div>
    <input id="carrier" type="text" :value="carrier" />
    <input id="phoneNumber" type="text" :value="phoneNumber" />
    <button @click="addAccount" type="button">add</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  props: {
    carrier: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
  },

  setup(props, context) {
    // const handleInput = (event: InputEvent) => {
    //   const eventTarget = event.target as HTMLInputElement
    //   context.emit("input", eventTarget.value)
    // }
    const addAccount = () => {
      context.emit("add")
    }

    return { addAccount }
  },
})
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
}
</style>
