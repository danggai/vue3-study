<template>
  <li>
    <span>{{ todoItem }}</span>
    <button @click="removeTodoItem">삭제</button>
  </li>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  props: {
    todoItem: String,
    index: Number,
  },
  setup(props, context) {
    const removeTodoItem = () => {
      console.log("index", props.index)
      context.emit("remove", props.index)
    }

    return { removeTodoItem }
  },
})
</script>

<style scoped></style>
