<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ sayhello }}</h2>
    <button @click="writeLog"><cite>{{ title }}1</cite></button>
  </div>
</template>

<script>
export default {
  name: 'AppSon',
  data () {
    return {
      msg: 'Welcome to Your Vue, MasterJ!',
      appSonMsg: 'AppSon.vue'
    }
  },
  props: [
    'sayhello',
    'title'
  ],
  methods: {
      writeLog () {
          console.log(this.sayhello);
          this.$emit('listenSth',this.appSonMsg);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  color: #42b983;
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
