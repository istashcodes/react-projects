<template>
  <div id="app">
    <Header />
    <TopicCard v-bind:topics="topics" />
  </div>
</template>

<script>
import TopicCard from '@/components/TopicCard.vue'
import Header from '@/components/layout/Header.vue'

export default {
  name: 'app',
  components: {
    Header,
    TopicCard
  },
  data() {
    return {
      topics: [
        {
          id: 1,
          title: 'Setting up the ground work',
          archived: false,
          description: 'we have to set up some ground work',
          expanded: false
        },
        {
          id: 2,
          title: 'Study Vue',
          archived: false,
          description: 'study vue courses and watch videos',
          expanded: false
        },
        {
          id: 3,
          title: 'Iterate on the designs',
          archived: false,
          description: 'prepare designs on figma and discuss',
          expanded: false
        }
      ]
    }
  }
}
</script>

<style>
/* #app {
 font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
} */

/* #nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
