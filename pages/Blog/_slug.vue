<template>
  <v-container v-if="post.data">
    <h1>{{ post.data.title }}</h1>
    <h4 v-if="post.data.author">
      {{ post.data.author.first_name }} {{ post.data.author.last_name }}
    </h4>
    <v-img
      class="mb-4"
      :src="post.data.featured_image"
      :alt="post.data.featured_image_alt"
      max-height="500"
      contain
    ></v-img>
    <v-divider></v-divider>
    <div v-html="post.data.body"></div>

    <router-link
      v-if="post.meta.previous_post"
      :to="/blog/ + post.meta.previous_post.slug"
      class="button"
    >
      {{ post.meta.previous_post.title }}
    </router-link>
    <v-spacer></v-spacer>
    <router-link
      v-if="post.meta.next_post"
      :to="/blog/ + post.meta.next_post.slug"
      class="button"
    >
      {{ post.meta.next_post.title }}
    </router-link>
  </v-container>
</template>

<script>
import Butter from 'buttercms'
const butter = Butter('916e0c9041fae7dad15987437aa6cef411ecf7aa')
export default {
  name: 'Post',
  data() {
    return {
      post: {},
    }
  },
  created() {
    this.getPost()
  },
  methods: {
    getPost() {
      butter.post.retrieve(this.$route.params.slug).then((res) => {
        this.post = res.data
      })
    },
  },
  head() {
    return {
      title: 'Blog Posts',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.$route.params.slug,
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped></style>
