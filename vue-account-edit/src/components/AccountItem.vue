<template>
  <div class="root">
    <img class="carrier" alt=" account logo" src="../assets/logo.png">
    <div class="body">
      <div class="horizontal">
        <p>{{ carrier }}</p>
        <img style="align-self: center margin-left: 10px" width="30" height="10"
          :class="isMain ? null : `hidden`" alt="main item"
          src="../assets/logo.png">
      </div>

      <p style="width: max-content;"> {{ phoneNumber }} </p>
    </div>

    <img class="tail" width="20" height="50" alt="detail" src="../assets/logo.png"
      @click="$emit('clickItemMenu')" style="cursor: pointer;">

  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'AccountItem',
  props: {
    carrier: {
      type: String,
      required: true,
    },
    isMain: {
      type: Boolean,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  emits: ["clickItemMenu"],
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.horizontal {
  display: flex;
}

.carrier {
  width: 60px;
  height: 60px;
  margin-right: 30px;
}

.root {
  display: flex;
  background: #eee;
  margin: 15px;
  padding: 10px 30px;
  border-radius: 10px;
  align-items: center;
}

.body {
  align-items: flex-start;
  margin-right: auto;
}

.tail {
  position: relative;
}

.hidden {
  display: none;
}

h1 {
  margin: 0 30px 40px 10px;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>