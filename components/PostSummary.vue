<template>
  <v-card class="mx-auto my-12" outlined>
    <v-img
      v-if="post.featured_image"
      contain
      :src="post.featured_image"
      max-height="350"
    ></v-img>
    <v-card-title>
      {{ post.title }}
    </v-card-title>
    <v-divider></v-divider>
    <v-card-text>
      {{ post.summary }}
      <v-divider></v-divider>
      Written By: {{ admin_full_name }}
    </v-card-text>
  </v-card>
</template>

<script>
import showdown from 'showdown'
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  computed: {
    admin_full_name() {
      return this.post.author.first_name + ' ' + this.post.author.last_name
    },
  },
  methods: {
    convertMarkdown(markdown) {
      const converter = new showdown.Converter()
      return converter.makeHtml(markdown)
    },
  },
}
</script>

<style lang="css" scoped>
.v-card__title {
  word-break: normal; /* maybe !important  */
}
</style>
