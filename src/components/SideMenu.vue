<template>
  <v-navigation-drawer :value="drawer" @click="closeDrawer" fixed app clipped class="drawer-style primary" id="style-1">
    <!--<v-toolbar-side-icon @click="closeDrawer" class="black&#45;&#45;text"></v-toolbar-side-icon>-->
    <v-list dense class="pt-3 white--text">
      <v-list-tile
        v-for="source in sources"
        :key="source.id"
      >
        <v-list-tile-action>
          <v-avatar size="32px">
            <img
              class="img-circle elevation-7 mb-1"
              :src="getImage(source.id)" />
          </v-avatar>

        </v-list-tile-action>

        <v-list-tile-content>
          <v-list-tile-title @click="setNews(source.id)">{{ source.name }}</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
  export default {
    name: 'SideMenu',
    props: {
      drawer: Boolean,
    },
    data() {
      return {
        sources: [],
        errors: [],
        localDrawer: this.drawer
      }
    },
    async created() {
      const newsAxios = await fetch(`${process.env.VUE_APP_NEWS_SOURCES}${process.env.VUE_APP_NEWS_API_KEY}`)
      const sourcesJSON = await newsAxios.json();
      this.sources = sourcesJSON.sources
    },
    methods: {
      closeDrawer() {
        this.$emit('setDrawerFalse', false)
      },
      getImage(id) {
        return require(`../assets/images/${id}.png`)
      },
      setNews(id) {
        this.$emit('setDrawerFalse', false)
        this.$emit('selectResource', id)
      }
    }
  }
</script>
