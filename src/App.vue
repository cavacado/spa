<template>
  <div>
    <v-container>
      <div id="app">
        <filterer v-on:triggerFilter='setFilter'></filterer>

        <v-progress-linear indeterminate v-if='!done'></v-progress-linear>
        <!-- <collection-wrapper>
          <collapsible-wrapper></collapsible-wrapper>
        </collection-wrapper> -->
        <v-collection v-for='(person,index) in API_DATA' v-if='done'>
          <v-collection-avatar v-bind:src="gitHub_API_DATA[index].data.avatar_url">
            <span class="title">gitHub Handle: <a v-bind:href='gitHub_API_DATA[index].data.html_url'>{{ person.githubLogin }}</a></span>

            <v-collapsible collapse>
              <li v-if="filter !== 'Project 2' && filter !== 'Project 3'">
                <v-collapsible-header>
                  <v-icon>filter_drama</v-icon> Project 1: {{ person.project1.repoName }}
                </v-collapsible-header>
                <v-collapsible-body>
                  <v-row>
                    <br>
                    <v-grid m3 ><img v-bind:src="person.project1.previewImage" class='round'></v-grid>
                    <v-grid m8>
                      Deployed URL: <a :href='person.project1.deployedUrl'>{{ person.project1.deployedUrl }}</a><br><br>
                      Repo URL: <a :href="'https://github.com/' + person.githubLogin + '/' + person.project1.repoName">{{ `https://github.com/${person.githubLogin}/${person.project1.repoName}` }}</a>
                    </v-grid>
                  </v-row>
                </v-collapsible-body>
              </li>
              <li v-if="filter !== 'Project 1' && filter !== 'Project 3'">
                <v-collapsible-header>
                  <v-icon>place</v-icon> Project 2: {{ person.project2.repoName }}
                </v-collapsible-header>
                <v-collapsible-body>
                  <v-row>
                    <br>
                    <v-grid m3 ><img v-bind:src="person.project2.previewImage" class='round'></v-grid>
                    <v-grid m8>
                      Deployed URL: <a :href='person.project2.deployedUrl'>{{ person.project2.deployedUrl }}</a><br><br>
                      Repo URL: <a :href="'https://github.com/' + person.githubLogin + '/' + person.project2.repoName">{{ `https://github.com/${person.githubLogin}/${person.project2.repoName}` }}</a>
                    </v-grid>
                  </v-row>
                </v-collapsible-body>
              </li>
              <li v-if="!!person.project3 && filter !== 'Project 1' && filter !== 'Project 2'">
                <v-collapsible-header >
                  <v-icon>whatshot</v-icon> Project 3: {{ person.project3.repoName }}
                </v-collapsible-header>
                <v-collapsible-body>
                  <v-row>
                    <br>
                    <v-grid m3 ><img v-bind:src="person.project3.previewImage" class='round'></v-grid>
                    <v-grid m8>
                      Deployed URL: <a :href='person.project3.deployedUrl'>{{ person.project3.deployedUrl }}</a></a><br><br>
                      Repo URL: <a :href="'https://github.com/' + person.githubLogin + '/' + person.project3.repoName">{{ `https://github.com/${person.githubLogin}/${person.project3.repoName}` }}</a>
                    </v-grid>
                  </v-row>
                </v-collapsible-body>
              </li>
            </v-collapsible>

          </v-collection-avatar>
        </v-collection>

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

export default {
  name: 'app',
  components: { filterer },
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
      const token = '1062ae6dd8d0f42742dd5fcde3c8de298f052a92';
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
}
.round {
  border-radius: 50%;
  width: 60px;
  height: 60px;
}
</style>
