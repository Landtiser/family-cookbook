<template>
  <main>
    <section v-if="posts" class="w-full max-w-5xl mx-auto">
      <h1 class="title">Ingredients</h1>
      <posts post-type="ingredients" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("ingredients").fetch();
    } catch (e) {
      error({ message: "Ingredients not found" });
    }
    return { posts };
  },
}
</script>
