<template>
  <div id="app">
      <div v-for="(item, i) in youtubeIdList" :key="i">
        <youtube :video-id="item" />
      </div> 
      

    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <button @click="AddVimeo">Add a video by entering vimeo video ID</button>:
    <input type="text" v-model="vimeoId">
    <hr>
    <div v-for="(item, i) in vimeoIdList" :key="i">
      <VimeoPart :id="item"></VimeoPart>
    </div> -->

    <a href="https://github.com/sunpochin/vue2-vimeo-player-cats-demo">source code</a>
    <br>
    <a href="https://vimeo-cat-dog.netlify.app/">Demo</a>
      
  </div>
</template>

<script>
// import VimeoPart from './components/VimeoPart.vue'
import axios from 'axios'

export default {
  data() {
    return {
      youtubeIdList: ['HlFgIBAm0Jg','OgyZIZMZAUM', 'UovBEFOgidI'],

      vimeoId: '',
      // 3 initial demo videos of cat and dog.
      vimeoIdList: ['807306477', '807306201', '192191']
    }
  },
  mounted() {
    console.log('mounted')
    axios
      .get('http://localhost:8000/tube?q=餵食')
      // .get('https://nodejs-video-api.onrender.com/tube?q=餵食')
      .then(response => {
        console.log('first: ' + response)
        console.log('data: ' + response.data)
      } )
  },

  methods: {
    AddVimeo() {
      this.vimeoIdList.push(this.vimeoId);
    },
  },
  name: 'App',
  // components: {
  //   VimeoPart
  // }
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
