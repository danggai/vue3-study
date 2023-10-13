<template>
  <div>
    <header>
      <h1>Vue 3 Todo With Typescript</h1>
    </header>
    <main>
      <todo-input
        :item="todoText"
        @input="updateTodoText"
        @add="addTodoItem"
      ></todo-input>
      <!-- <todo-input v-model="todoText" @add="addTodoItem"></todo-input> -->
      <div>
        <todo-list-item
          v-for="(todoItem, index) in todoItems"
          :key="index"
          :todoItem="todoItem"
          :index="index"
          @remove="removeTodoItem"
        ></todo-list-item>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import { ref } from "vue"
import TodoInput from "./components/TodoInput.vue"
import TodoListItem from "./components/TodoListItem.vue"

const STROAGE_KEY = "vue-todo-ts-v1"
const storage = {
  save(todoItems: any[]) {
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STROAGE_KEY, parsed)
  },

  fetch() {
    const todoItems = localStorage.getItem(STROAGE_KEY) || "[]"
    const result = JSON.parse(todoItems)
    return result
  },
}

export default {
  components: { TodoInput, TodoListItem },
  setup() {
    const todoText = ref("")
    const todoItems = ref([] as any[])

    // const updateTodoText = (value: string) => {
    //   todoText.value = value
    // }
    const updateTodoText = (event: InputEvent) => {
      const eventTarget = event.target as HTMLInputElement
      todoText.value = eventTarget.value
    }

    const addTodoItem = () => {
      const value = todoText.value
      todoItems.value.push(value)
      storage.save(todoItems.value)
      initTodoText()
    }

    const initTodoText = () => {
      todoText.value = ""
    }

    const fetchTodoItems = () => {
      todoItems.value = storage.fetch()
    }

    const removeTodoItem = (index: number) => {
      todoItems.value.splice(index, 1)
      storage.save(todoItems.value)
    }

    fetchTodoItems()

    return {
      todoText,
      todoItems,
      updateTodoText,
      addTodoItem,
      fetchTodoItems,
      removeTodoItem,
    }
  },
}
</script>

<style scoped></style>
