<!-- eslint-disable prettier/prettier -->
<template>
  <li>
    <span
      class="item"
      :class="todoItem?.done ? `complete` : null"
      @click="toggleItem"
    >{{ todoItem?.title }}</span>
    <button @click="removeTodoItem">삭제</button>
  </li>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue"
import { Todo } from "../App.vue"

export default defineComponent({
  props: {
    todoItem: Object as PropType<Todo>,
    index: Number,
  },
  setup(props, context) {
    const removeTodoItem = () => {
      context.emit("remove", props.index)
    }

    const toggleItem = () => {
      context.emit("toggle", props.todoItem, props.index)
    }
    return { removeTodoItem, toggleItem }
  },
})
</script>

<style scoped>
.item {
  cursor: pointer;
  padding-right: 10px;
}

.complete {
  text-decoration: line-through;
  color: gray;
}
</style>
