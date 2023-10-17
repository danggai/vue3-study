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
          @toggle="toggleTodoItem"
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
  save(todoItems: Todo[]) {
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STROAGE_KEY, parsed)
  },

  fetch(): Todo[] {
    const todoItems = localStorage.getItem(STROAGE_KEY) || "[]"
    const result = JSON.parse(todoItems).sort()
    return result
  },
}

export interface Todo {
  title: string
  done: boolean
  // id: number
}

export default {
  components: { TodoInput, TodoListItem },
  setup() {
    const todoText = ref("")
    const todoItems = ref([] as Todo[])

    // const updateTodoText = (value: string) => {
    //   todoText.value = value
    // }
    const updateTodoText = (event: InputEvent) => {
      const eventTarget = event.target as HTMLInputElement
      todoText.value = eventTarget.value
    }

    const addTodoItem = () => {
      const todo: Todo = {
        title: todoText.value,
        done: false,
      }
      todoItems.value.push(todo)
      storage.save(todoItems.value)
      initTodoText()
    }

    const initTodoText = () => {
      todoText.value = ""
    }

    const fetchTodoItems = () => {
      todoItems.value = storage.fetch().sort((a, b) => {
        if (a.title < b.title) return -1
        if (a.title > b.title) return 1
        return 0
      })
    }

    const removeTodoItem = (index: number) => {
      todoItems.value.splice(index, 1)
      storage.save(todoItems.value)
    }

    const toggleTodoItem = (todoItem: Todo, index: number) => {
      console.log(todoItem)
      todoItems.value.splice(index, 1, {
        ...todoItem,
        done: !todoItem.done,
      })
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
      toggleTodoItem,
    }
  },
}
</script>

<style scoped></style>
