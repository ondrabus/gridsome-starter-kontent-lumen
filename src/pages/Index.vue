<template>
  <Layout>
    <Sidebar :isHomePage="true" :routeParams="this.$route.params" />
    <div class="content">
      <div class="content__inner">
        <Article v-for="article in $page.allArticle.edges" v-bind:key="article.node.id" :article="article.node" />
      </div>
    </div>
  </Layout>
</template>

<script>
import Article from "~/components/article.vue"
import Sidebar from "~/components/sidebar.vue"

export default {
  components: {
    Article,
    Sidebar
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<page-query>
query MyQuery {
  allArticle(sortBy: "date1", order: DESC) {
    edges {
      node{
        id,
        date1,
        path,
        category {
          slug
          title
        },
        description,
        title
      }
    }
  }
}
</page-query>