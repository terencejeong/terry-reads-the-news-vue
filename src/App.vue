<template>
  <v-app light>
    <SideMenu
      :drawer="drawer"
      @setDrawerFalse='drawer = $event'
      @selectResource="setResource">
    </SideMenu>
    <v-toolbar fixed app light clipped-left color="primary" class="elevation-2">
      <v-toolbar-side-icon @click="drawer = !drawer" class="white--text"></v-toolbar-side-icon>
      <v-toolbar-title class="white--text">Terry's News Summary</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
            <v-progress-circular
              color="primary"
              indeterminate
              v-if="isLoading"
            ></v-progress-circular>
        </v-layout>
        <MainContent :articles="articles" v-if="!isLoading" />
      </v-container>
    </v-content>
  </v-app>

</template>
<script>
  import SideMenu from './components/SideMenu.vue'
  import MainContent from './components/MainContent.vue'

  export default {
    components: {
      SideMenu,
      MainContent
    },
    data () {
      return {
        drawer: false,
        articles: [],
        isLoading: true,
      }
    },
    async created() {
      this.setResource('abc-news-au')
    },
    methods: {
      drawerOpen() {
        this.drawer = false
      },
      async setResource(resource) {
        this.isLoading = true;
        const newsHeadlinesFetch = await fetch(`https://newsapi.org/v2/top-headlines?sources=${resource}&apiKey=${process.env.VUE_APP_NEWS_API_KEY}`);
        const newsHeadlines = await newsHeadlinesFetch.json();
        this.articles = newsHeadlines.articles;
        this.isLoading = false;
      }
    },
    // watch: {
    //   drawer() {
    //     console.log(this.drawer)
    //   }
    // }
  }
</script>
