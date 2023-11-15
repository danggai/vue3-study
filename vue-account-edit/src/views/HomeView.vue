<template>
  <div class="home">
    <input id="carrier" type="text" v-model="carrier" placeholder="carrier" />
    <input id="phoneNumber" type="text" v-model="phoneNumber"
      placeholder="phone number" />
    <button @click="addDummyAccount" type="button">add</button>

    <!-- <add-account @add="addTodoItem" :carrier="carrier"
      :phone-number="phoneNumber" /> -->

    <account-item v-for="(accountItem, index) in accountItems" :key="index"
      :carrier="accountItem.carrier" :phoneNumber="accountItem.phoneNumber"
      :isMain="accountItem.isMain" :index="index" @clickItemMenu="open(index)" />


    <div class="bottomButton">
      <p style="width: auto; text-align: center;" @click="addAccount()"> 충전수단 추가하기
      </p>
    </div>

    <template>
      <vue-bottom-sheet ref="myBottomSheet">
        <div>
          <p style="margin-right: 20px; text-align: right; cursor: pointer;"
            @click="close()">
            close
          </p>
        </div>

        <p style="margin: 20px; cursor: pointer" @click="setMainAccount()">
          대표계좌설정
        </p>

        <p style="margin: 20px; cursor: pointer" @click="deleteAccount()">
          삭제
        </p>
      </vue-bottom-sheet>
    </template>
  </div>
</template>
  
<script lang="ts">
import AccountItem from '../components/AccountItem.vue';
import { defineComponent, ref } from 'vue'

const STROAGE_KEY = "vue-todo-ts-v1"
const storage = {
  save(todoItems: Account[]) {
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STROAGE_KEY, parsed)
  },

  fetch(): Account[] {
    const todoItems = localStorage.getItem(STROAGE_KEY) || "[]"
    const result = JSON.parse(todoItems).sort()
    return result
  },
}

export interface Account {
  carrier: string
  phoneNumber: string
  isMain: boolean
}

export default defineComponent({
  name: 'HomeView',
  components: {
    AccountItem,
  },
});
</script>

<script setup lang="ts">
import VueBottomSheet from "@webzlodimir/vue-bottom-sheet";
import "@webzlodimir/vue-bottom-sheet/dist/style.css";


const myBottomSheet = ref<InstanceType<typeof VueBottomSheet>>()
const carrier = ref("")
const phoneNumber = ref("")
const accountItems = ref([] as Account[])
const selectedIndex = ref(-1)

const addDummyAccount = () => {
  const account: Account = {
    carrier: carrier.value,
    phoneNumber: phoneNumber.value,
    isMain: false,
  }
  accountItems.value.push(account)
  storage.save(accountItems.value)

  alert("계좌추가완료!")

  initTodoText()
}

const addAccount = () => {
  console.log(3434)
}

const setMainAccount = () => {
  const index = selectedIndex.value

  if (index >= 0 && index < accountItems.value.length) {
    accountItems.value.forEach((item, i) => {
      if (i === index) {
        item.isMain = true;
      } else {
        item.isMain = false;
      }
    });
  }

  storage.save(accountItems.value)
  close()
}

const deleteAccount = () => {
  const index = selectedIndex.value

  accountItems.value.splice(index, 1)

  storage.save(accountItems.value)
  close()
}

const initTodoText = () => {
  carrier.value = ""
  phoneNumber.value = ""
}

const fetchTodoItems = () => {
  accountItems.value = storage.fetch().sort((a, b) => {
    if (a.phoneNumber < b.phoneNumber) return -1
    if (a.phoneNumber > b.phoneNumber) return 1
    return 0
  })
}

const open = (index: number) => {
  if (myBottomSheet.value != null) {
    selectedIndex.value = index
    myBottomSheet.value.open();
  }
}

const close = () => {
  if (myBottomSheet.value != null) {
    selectedIndex.value = -1
    myBottomSheet.value.close();
  }
}

fetchTodoItems()

</script>

<style scoped>
.bottomButton {
  position: absolute;
  bottom: 30px;
  right: 30px;
  left: 30px;
  width: auto;
  background: #eee;
  border-radius: 10px;
  align-items: center;
  cursor: pointer;
}
</style>