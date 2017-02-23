<template>
  <div>
    <v-collection v-for='(person,index) in aData' v-if='done'>
      <v-collection-avatar v-bind:src="gData[index].data.avatar_url">
        <span class="title">gitHub Handle: <a v-bind:href='gData[index].data.html_url'>{{ person.githubLogin }}</a></span>
        <collapsible-wrapper :person-data='person' :filter='filter' ></collapsible-wrapper>
      </v-collection-avatar>
    </v-collection>
  </div>
</template>

<script>
  import collapsibleWrapper from './CollapsibleWrapper.vue';

  export default {
    name: 'collection-wrapper',
    props: [ 'aData', 'gData', 'done', 'filter' ],
    components: { collapsibleWrapper },
    data: function() {
      return {

      }
    }
  }
</script>

<style scoped></style>
