<template>
  <div>
    <h1 class="title is-1">
      Articles
    </h1>
    <hr>
    <div
      v-for="(article, index) in articles"
      :key="index"
      class="content is-medium"
    >
      <h2 class="subtitle is-4">
        {{ formatDate(article.updatedAt) }}
      </h2>
      <h1 class="title">
        {{ article.title }}
      </h1>
      <p>
        {{ article.description }}
      </p>
      <NuxtLink
        :to="'articles/' + article.slug"
      >
        Read Article <i class="fas fa-book-open" />
      </NuxtLink>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const articles = await $content('articles').fetch()
    return { articles }
  },
  methods: {
    formatDate (date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>
