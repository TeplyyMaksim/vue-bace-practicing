<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      <input type="text" v-model="title">
    </div>
    <div v-once>
      Initial title: {{title}}
    </div>
    <div>
      Single title: {{title}}
    </div>
    <div>
      Naruto style title: {{title + " datebayo"}}
    </div>
    <div>
      Square title: {{generator()}}
    </div>
    <hr>

    <div>
      I did it megasite using <a :href="link" target="_blank">this</a> site
    </div>
    <div>
      It is <span v-html="htmledLink"></span>, if you do not got a Joke
    </div>
    <hr>

    <p>{{countChecker}}</p>
    <p>Counter: {{counter}}</p>
    <button @click="increaseCounter(2, $event)">Increase by two</button>
    <button @click="counter += 1">Increment</button>
    <button @click="counter -= 1">Decrement</button>
    <p @mousemove="setMoveCoordinates">
      Coordinates: {{getMoveCoordinates()}} <span class="dead-spot" @mousemove.stop>DEAD SPOT</span>
    </p>
    <div>
      Input s/g and press enter <input type="text" @keyup.enter.space="alerter">
    </div>
    <hr>

    <div class="demo-block" @click="attachedCrimson = !attachedCrimson" :class="firstBlockClasses">Alpha</div>
    <div class="demo-block" :style="{backgroundColor: color}">Beta</div>
    <div class="demo-block" :class="['yellow-block', 'orange-text']">Gamma</div><br>
    <input type="color" v-model="color">
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      title: 'Rewrite me using input',

      link: 'http://google.com',
      htmledLink: '<a href="http://google.com" target="_blank">Google</a>',

      counter: 0,
      xCoord: 0,
      yCoord: 0,

      attachedCrimson: false,
      color: '#000000',
    };
  },
  computed: {
    countChecker() {
      return this.counter > 5 ? 'Greater then 5' : 'Less/equal 5';
    },
    firstBlockClasses() {
      return {
        'crimson-block': this.attachedCrimson,
        'black-block': !this.attachedCrimson,
      };
    },
  },
  watch: {
    counter() {
      // Asyncronous task allowed here but not in computed
      setTimeout(() => {
        this.counter = 0;
      }, 2000);
    },
  },
  methods: {
    generator() {
      return `${this.title} ${this.title}`;
    },
    increaseCounter(num) {
      // Event comes as second parameter
      this.counter += num;
    },
    setMoveCoordinates(event) {
      this.xCoord = event.clientX;
      this.yCoord = event.clientY;
    },
    getMoveCoordinates() {
      return `${this.xCoord} / ${this.yCoord}`;
    },
    /* Hard way to stop bubling event */
    // deadSpot(event) {
    //   event.stopPropagation();
    // },
    alerter(event) {
      alert(event.target.value);
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 10px;
}
.dead-spot {
  background: crimson;
}
.demo-block {
  width: 100px;
  height: 100px;
  background: darkgrey;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
}
.crimson-block {
  background: crimson;
}
.black-block {
  background: black;
}
.yellow-block {
  background: yellow;
}
.orange-text {
  color: orange;
}
</style>
