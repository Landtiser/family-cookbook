<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title">Recipes</h1>
      <posts post-type="recipes" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("recipes").fetch();
    } catch (e) {
      error({ message: "Recipes not found" });
    }
    return { posts };
  },
}
</script>
