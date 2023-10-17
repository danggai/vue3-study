<!-- eslint-disable prettier/prettier -->
<template>
  <div>
    <label for="todo-input">오늘 할 일 : </label>
    <!-- input 컴포넌트에서의 @input <~ 값 변화시마다 발동하는 이벤트 -->
    <input
      id="todo-input"
      type="text"
      :value="item"
      @input="handleInput"
    />
    <button
      @click="addTodo"
      type="button"
    >add</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  // props: ["item"],
  props: {
    item: {
      type: String,
      required: true,
    },
  },

  setup(props, context) {
    // const handleInput = (event: InputEvent) => {
    //   const eventTarget = event.target as HTMLInputElement
    //   context.emit("input", eventTarget.value)
    // }
    const handleInput = (event: Event) => {
      context.emit("input", event)
    }

    const addTodo = () => {
      context.emit("add")
    }

    return { addTodo, handleInput }
  },
})
</script>

<style scoped></style>
