<template>
  <div id="app">
    <div>
      <button @click="authorize">登入 Google</button>
    </div>

    <!-- <button @click="searchCourse">Search Course</button>:
    <input type="text" v-model="searchString"> -->
    <br>


    <!-- <button @click="AddYoutube">Add a video by entering video ID</button>:
    <input type="text" v-model="videoId"> -->

    <!-- <div v-for="(item, i) in youtubeIdList" :key="i">
      <youtube :video-id="item" />
    </div> -->


    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <hr>
    <!-- <div v-for="(item, i) in vimeoIdList" :key="i">
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
      // 3 initial demo videos of cat and dog.
      searchString: '餵食貓咪',
      // youtubeIdList: ['HlFgIBAm0Jg','OgyZIZMZAUM', 'XcDtulLcrbU'],
      youtubeIdList: [],

      videoId: '',
      // 3 initial demo videos of cat and dog.
      vimeoIdList: ['807306477', '807306201', '192191']
    }
  },
  mounted() {
    console.log('mounted')
//    this.searchCourse();
  },

  methods: {
    authorize() {
      window.location.href = "http://localhost:8000/auth/google"; // Node.js 授權路由
    },

    async searchCourse() {
      console.log('call Axios')

      const ret = await axios
        .get('http://localhost:8000/tube?act=search&q=' + this.searchString)
//        .get('https://nodejs-video-api.onrender.com/tube?act=search&q=餵食')
        .then((res) => {
          console.log('data: ' + res.data)
          console.log('data 0: ' + res.data[0])

          // let data0 = res.data[0];
          // const idx = data0.indexOf('watch?v=');
          // console.log('idx: ', idx, ', data0.length: ', data0.length)
          // let result = data0.substring(idx + 8, data0.length - 2);
          // console.log('result: ', result)
          // this.youtubeIdList.push(result);
          this.youtubeIdList.splice(0, this.youtubeIdList.length); 

          res.data.forEach((data) => {
            const idx = data.indexOf('watch?v=');
            console.log('idx: ', idx, ', data0.length: ', data.length)
            let result = data.substring(idx + 8, data.length - 2);
            console.log('result: ', result)
            this.youtubeIdList.push(result);
          })


        } ) 
      console.log('ret: ', ret)
    },
    AddVimeo() {
      this.vimeoIdList.push(this.videoId);
    },
    AddYoutube() {
      this.youtubeIdList.push(this.videoId);
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
