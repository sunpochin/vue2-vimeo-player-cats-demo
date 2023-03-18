<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <input type="text" v-model="vimeoId">
    <button @click="AddVimeo">Add a video by entering vimeo video ID</button>
    <div v-for="(item, i) in vimeoIdList" :key="i">
      <VimeoPart :id="item"></VimeoPart>
    </div>
  </div>
</template>

<script>
import VimeoPart from './components/VimeoPart.vue'

export default {
  data() {
    return {
      vimeoId: '',
      // 3 initial demo videos of cat and dog.
      vimeoIdList: [807306477, 807306201, 192191]
    }
  },
  methods: {
    AddVimeo() {
      this.vimeoIdList.push(this.vimeoId);
    },
  },
  name: 'App',
  components: {
    VimeoPart
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
