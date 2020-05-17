<template>
  <div>
    <ul>
      <li
        v-for="post in posts"
        :key="post.frontmatter.date"
      >
        <div>
          <div>
            <RouterLink
              :to="post.path"
            >
              {{ post.title }}
            </RouterLink>
            <div v-html="post.excerpt"></div>
            <RouterLink
              :to="post.path"
            >
              <span>Read more</span>
            </RouterLink>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Homepage",

  computed: {
    posts() {
      return this.$site.pages
        .filter(
          x =>
            x.path.startsWith("/pages/") &&
            !x.frontmatter.blog_index &&
            x.frontmatter.layout !== "About" &&
            new Date(x.frontmatter.date) < new Date()
        )
        .sort(
          (a, b) => new Date(b.frontmatter.date) - new Date(a.frontmatter.date)
        );
    }
  }
};
</script>