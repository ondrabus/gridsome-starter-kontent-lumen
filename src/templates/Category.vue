<template>
  <Layout>
    <Sidebar :isHomePage="true" :routeParams="this.$route.params" />
    <div class="content">
      <div class="content__inner">
        <Article v-for="article in articles" v-bind:key="article.node.id" :article="article.node" />
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
  metaInfo() {
    return {
      title: `${this.$page.category.title} - ${this.$page.allSiteMetadata.edges[0].node.title}`
    }
  },
  computed: {
    articles: function(){
      return this.$page.allArticle.edges.filter(e => e.node.category.find(c => c.slug == this.$page.category.slug));
    }
  }
}
</script>

<page-query>
query MyQuery ($id: ID!) {
  category(id: $id){
    title
    slug
  }
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
  allSiteMetadata(limit: 1) {
    edges
    {
      node {
        title
        subtitle
      }
    }
  }
}
</page-query>