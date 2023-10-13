<template>
  <div>
    <AppHeader 
    :appTitle="msg" 
    v-on:change="changeTitle">
  </AppHeader>
  <button @click="showAlert">경고</button>
</div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';

export default {
  components: {
    'AppHeader': AppHeader,
  },
  data() {
    return {
      msg: "앱 헤더 컴포넌트"
    }
  },
  methods: {
    showAlert() {
      alert("hello")
    },
    changeTitle() {
      this.msg = "새로운 " + this.msg
    }
  },
}
</script>

<style scoped>

</style>