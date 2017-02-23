<template>
  <div>
    <v-collapsible collapse>
      <li v-if="filter !== 'Project 2' && filter !== 'Project 3'">
        <v-collapsible-header>
          <v-icon>filter_drama</v-icon> Project 1: {{ personData.project1.repoName }}
        </v-collapsible-header>
        <v-collapsible-body>
          <v-row>
            <br>
            <v-grid m3 ><img v-bind:src="personData.project1.previewImage" class='round'></v-grid>
            <v-grid m8>
              Deployed URL: <a :href='personData.project1.deployedUrl'>{{ personData.project1.deployedUrl }}</a><br><br>
              Repo URL: <a :href="'https://github.com/' + personData.githubLogin + '/' + personData.project1.repoName">{{ `https://github.com/${personData.githubLogin}/${personData.project1.repoName}` }}</a>
            </v-grid>
          </v-row>
        </v-collapsible-body>
      </li>
      <li v-if="filter !== 'Project 1' && filter !== 'Project 3'">
        <v-collapsible-header>
          <v-icon>place</v-icon> Project 2: {{ personData.project2.repoName }}
        </v-collapsible-header>
        <v-collapsible-body>
          <v-row>
            <br>
            <v-grid m3 ><img v-bind:src="personData.project2.previewImage" class='round'></v-grid>
            <v-grid m8>
              Deployed URL: <a :href='personData.project2.deployedUrl'>{{ personData.project2.deployedUrl }}</a><br><br>
              Repo URL: <a :href="'https://github.com/' + personData.githubLogin + '/' + personData.project2.repoName">{{ `https://github.com/${personData.githubLogin}/${personData.project2.repoName}` }}</a>
            </v-grid>
          </v-row>
        </v-collapsible-body>
      </li>
      <li v-if="!!personData.project3 && filter !== 'Project 1' && filter !== 'Project 2'">
        <v-collapsible-header >
          <v-icon>whatshot</v-icon> Project 3: {{ personData.project3.repoName }}
        </v-collapsible-header>
        <v-collapsible-body>
          <v-row>
            <br>
            <v-grid m3 ><img v-bind:src="personData.project3.previewImage" class='round'></v-grid>
            <v-grid m8>
              Deployed URL: <a :href='personData.project3.deployedUrl'>{{ personData.project3.deployedUrl }}</a></a><br><br>
              Repo URL: <a :href="'https://github.com/' + personData.githubLogin + '/' + personData.project3.repoName">{{ `https://github.com/${personData.githubLogin}/${personData.project3.repoName}` }}</a>
            </v-grid>
          </v-row>
        </v-collapsible-body>
      </li>
    </v-collapsible>
  </div>
</template>

<script>
  export default {
    name: 'collapsible-wrapper',
    props: [ 'personData', 'filter' ],
    data: function() {
      return {

      }
    }
  }
</script>

<style scoped></style>
