<template> 

  <div id="sorting" :style="{height: height + 'px', width: width + 'px'}">
    <div class="bar" v-for="(number, index) in array" :key="index" :style="{height: (number/(size/100)) +'%', width: (100/size) + '%'}" />
  </div>

  <button @click="shuffleArray()">Shuffle</button>

  <button @click="bubbleSort()">Bubble Sort</button>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      array: [],
      width: document.documentElement.clientWidth,
      height: document.documentElement.clientHeight*0.8,
      size: window.screen.availWidth/1.5

    }
  },

  methods: {

    shuffleArray() {
      for (let i = this.array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.array[i], this.array[j]] = [this.array[j], this.array[i]];
      }
    },

    fillArray() {
      for (let i = 0; i < this.size; i++) {
        this.array.push(i)
      }
      this.shuffleArray()
    },

    sleep(e=1) {
      return new Promise((resolve) => setTimeout(resolve,e));
    },

    async bubbleSort(){

      let len = this.array.length
      let checked;
      do {
        checked = false;
        for(let i =0;i<len;i++){
          if(this.array[i] > this.array[i+1]){
            let tmp = this.array[i];
            this.array[i] = this.array[i+1];
            this.array[i+1] = tmp;
            // sleep - to visualize / see the changes
            checked = true;
          }
        } await this.sleep()
      } while (checked)
    },

  },

  created() {
    this.fillArray();
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
  margin-top: 20px;
}

.bar {
  display: inline-block;
  background-color: black;
}

</style>