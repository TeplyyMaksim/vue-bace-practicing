<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      <input type="text" @input="changeTitle">
    </div>
    <div v-once>
      Initial title: {{title}}
    </div>
    <div>
      Single title: {{title}}
    </div>
    <div>
      Square title: {{generator()}}
    </div>
    <hr>
    <div>
      I did it megasite using <a :href="link" target="_blank" @click="resetTitle">this</a> site
    </div>
    <div>
      It is <span v-html="htmledLink"></span>, if you do not got a Joke
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      title: 'Rewrite me using right input',
      link: 'http://google.com',
      htmledLink: '<a href="http://google.com" target="_blank">Google</a>',
    };
  },
  methods: {
    changeTitle(event) {
      this.title = event.target.value;
    },
    generator() {
      return `${this.title} ${this.title}`;
    },
    resetTitle() {
      this.title = 'Reseted';
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}
</style>
