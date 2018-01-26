<template>
  <div class="container" id="app">
    <SourceSelection @sourceChanged="sourceChanged">
    </SourceSelection>
    <Newslist :source="source"></Newslist>
  </div>
</template>

<script>
import Newslist from './components/Newslist'
import SourceSelection from './components/SourceSelection'

export default {
  name: 'app',
  components: {
    Newslist,
    SourceSelection
  },
  data () {
    return {
      source: ''
    }
  },
  methods: {
    sourceChanged: function (source) {
      this.source = source
    }
  }
}
</script>

<style lang="scss">
html, body {
  margin: 0;
  padding: 0;
}

body {
  background: #f8f8f8;
}

a {
  color: darken(cornflowerblue, 10%);
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.button {
  background: cornflowerblue;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
  font-size: 14px;
}

.form {
  &__select {
    font-size: 16px;
    height: 30px;
    outline: none;
  }
}
</style>
