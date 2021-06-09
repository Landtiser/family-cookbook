<template>
  <main>
    <section v-if="post">
      <nav class="mb-8" aria-label="go back">
        <router-back class="block" />
      </nav>

      <article>
        <h5
          v-if="post.createdAt"
          class="inline-block py-1 px-2 my-2 bg-gray text-white text-sm font-medium rounded-sm whitespace-no-wrap"
        >{{ formatDate(post[0].createdAt) }}</h5>
        <h1 class="">{{ post[0].title }}</h1>
        <p class="mt-1 mb-4 text-primary-600 dark:text-primary-400">{{ post[0].description }}</p>
        <ul>
          <li :key="ingredient.ingredient" v-for="ingredient in post[0].ingredients">{{ingredient.ingredient}}, {{ingredient.amount.number}} {{ingredient.amount.unit}}</li>
        </ul>
        <nuxt-content :document="post[0]" />
      </article>
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("recipes", params.slug).fetch();
      console.log(post);
    } catch (e) {
      error({ message: "Recipe not found" });
    }
    return { post };
  },
  methods: {
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString(process.env.lang) || ''
    }
  }
}
</script>
