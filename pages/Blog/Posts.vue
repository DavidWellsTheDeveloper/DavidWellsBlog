<template>
  <div>
    <v-container>
      <v-row>
        <v-col v-for="post in posts" :key="post.id" cols="12" md="6" lg="4">
          <PostSummary :post="post" />
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <p>Blog powered by:</p>
      <a href="https://buttercms.com/">
        <v-img src="/butter-y.png" max-width="200"></v-img>
      </a>
    </v-container>
  </div>
</template>

<script>
// import axios from 'axios'
import PostSummary from '@/components/PostSummary.vue'
import Butter from 'buttercms'
const butter = Butter('916e0c9041fae7dad15987437aa6cef411ecf7aa')
export default {
  name: 'BlogPosts',
  components: {
    PostSummary,
  },
  data() {
    return {
      posts: {},
    }
  },
  computed: {
    name() {
      return this.data
    },
  },
  mounted() {
    butter.post
      .list({
        page: 1,
        page_size: 10,
      })
      .then((res) => {
        this.posts = res.data.data
      })
  },
  head() {
    return {
      title: 'Blog Posts',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'See popular & trending posts about the Colorado Avalanche',
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped></style>
