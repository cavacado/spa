<template>
  <div>
    <v-container>
      <div id="app">
        <filterer v-on:triggerFilter='setFilter'></filterer>
        <v-progress-linear indeterminate v-if='!done'></v-progress-linear>
        <transition name='fade'>
          <collection-wrapper v-if='done' :a-data='API_DATA' :g-data='gitHub_API_DATA' :done='done' :filter='filter'></collection-wrapper>
        </transition>
      </div>
    </v-container>
    <v-footer class='teal'>
      <div class="container" slot="copyright">&copy; Vue Copyright 2017</div>
    </v-footer>
  </div>
</template>

<script>
import axios from 'axios';
import filterer from './components/Filter.vue';
import collectionWrapper from './components/CollectionWrapper.vue';

export default {
  name: 'app',
  components: { filterer, collectionWrapper },
  data: function() {
    return {
      API_PATH: 'https://raw.githubusercontent.com/wdi-sg/alumni/master/data.json',
      API_DATA: '',
      gitHub_API_PATH: 'https://api.github.com/users/',
      gitHub_API_DATA: [],
      done: false,
      filter: ''
    }
  },
  methods: {
    setFilter: function() {
      this.filter = arguments[0]
    }
  },
  computed: {
  },
  created: function() {
      const token = process.env.token;
      let vm = this;
      let promises = [];
      axios.get(vm.API_PATH).then(function(response) {
        vm.API_DATA = response.data
        response.data.map(function(value,index){
          promises.push(axios.get(`${vm.gitHub_API_PATH}${value.githubLogin}?access_token=${token}`));
        })
        axios.all(promises).then(function(results){
          vm.gitHub_API_DATA = results;
          vm.done = true
        })
      })
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
  font-size: larger;
}
.round {
  border-radius: 50%;
  width: 60px;
  height: 60px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 2s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}
</style>
