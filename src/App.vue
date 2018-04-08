<template>
  <div id="app">
    <img src="./assets/logo.png">
    <upload :files="files" @changeFile="changeFile"></upload>
  </div>
</template>

<script>
import upload from './components/upload'

export default {
  name: 'App',
  data () {
    return {
      files: [
        {
          text: '1.jpg'
        }
      ]
    }
  },
  methods: {
    changeFile (files) {
      this.files = files
      console.log(this.files)
    }
  },
  components: {
    upload
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
