<template>
  <v-app>
      <Header/>
      <Content/>
  </v-app>
</template>

<script>
import Header from './components/Header';
import Content from './components/Content';


export default {
  name: 'App',
  components: {
    Header,
    Content,
  },

  data: () => ({
    //
  }),
};
</script>
