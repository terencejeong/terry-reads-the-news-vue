<template>
  <v-layout row wrap align-center>
    <v-flex :class="isMobile"  offset-md2>
      <h1 style="text-align: center; color: rgba(0,0,0,0.87)">{{articles[0].source.name}}</h1>
      <div v-for="article in articles" :key="article.title">
        <v-card class="my-3" hover data-aos="zoom-in" data-aos-easing="ease">
          <v-img
            height="350px"
            :src="article.urlToImage"
          ></v-img>
          <v-container fill-height fluid>
            <v-layout>
              <v-flex xs12 align-end d-flex>
                <span class="headline">{{ article.title }}</span>
              </v-flex>
            </v-layout>
          </v-container>
          <v-card-text>
            {{ article.description }}
          </v-card-text>
          <v-card-actions>
            <v-chip small color="secondary" class="white--text">
              {{article.source.name}}
            </v-chip>
            <v-spacer></v-spacer>
            <v-btn small replace color="info" :href="article.url" target="_blank">Read More</v-btn>
          </v-card-actions>
        </v-card>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    props: {
      articles: Array,
    },
    mounted() {
      return window.scrollTo(0,0);
    },
    computed: {
      isMobile: () => {
        return {
          'xs8': screen.width > 760,
          'xs12': screen.width < 760
        }
      }
    }
  }
</script>



