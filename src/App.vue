<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="undo-redo-app">
      <h1>Undo/Redo APP</h1>
      <input type="text" v-model="textInput">
      <h3>Output: {{textInput}}</h3>
      <button v-on:click="reverse()">Reverse</button>
      <button v-on:click="undoRedo">Undo/Redo</button>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  data : ()=>{
    return {
      textInput : '',
      textInputBackup: '',
      clickCount : 0,
      timer : null,
      clickTimer: null,
      clickType : true,
    }
  },
  props: {
    tag: {
      type: String,
      default: 'a'
    },
    delay: {
      type: Number,
      default: 250
    }
  },
  methods : {
    reverse(){
      this.textInput = this.textInput.split('').reverse().join('');
    },
    undoRedo : function(e){
      var self = this;
      e.preventDefault()
      this.clickCount++
      // console.log(this.clickCount++)
      this.textInputBackup = this.textInput;
      if (this.clickCount === 1) {
              this.clickTimer = setTimeout(() => {
                this.clickCount = 0
                this.clickType = true;
                this.textInput = this.textInput.slice(0, -1);
                console.log('singleclick')
              }, this.delay)
            } else if (this.clickCount === 2) {
              clearTimeout(this.clickTimer)
              this.clickCount = 0
              this.clickType = false;
              console.log('double-click')
            }
    }
  },
  components: {
    HelloWorld
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
}

#app {
  position: relative;
  height: 100vh;
}

body {
  margin: 0;
}

.undo-redo-app {
  width: 300px;
  min-height: 420px;
  border: 1px solid #ccc;
  position: absolute;
  top:0;
  left: 50%;
  transform: translate(-50%, 20%);
  padding: 0 20px;
  border-radius: 4px;
}


input, button {
  padding: 8px 20px;
}

button {
  margin-left: 15px;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
ul li {
  padding: 8px 0;
}
b {
  margin-top: 20px;
}
</style>
