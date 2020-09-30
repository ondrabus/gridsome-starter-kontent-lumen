<template>
  <Layout>
    <Sidebar :isHomePage="true" :routeParams="this.$route.params" />
    <div class="content">
      <div class="content__inner">
        <div class="page">
            <h1 class="page__title">
              All Articles tagged as &quot;{{$page.tag.title}}&quot;
            </h1>
            <div className="page__body">
              <Article v-for="article in articles" v-bind:key="article.node.id" :article="article.node" />
            </div>
          </div>
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
      title: `All Articles tagged as "${this.$page.tag.title}" - ${this.$page.allSiteMetadata.edges[0].node.title}`
    }
  },
  computed: {
    articles: function(){
      return this.$page.allArticle.edges.filter(e => e.node.tags.find(t => t.slug == this.$page.tag.slug));
    }
  }
}
</script>

<page-query>
query MyQuery ($id: ID!) {
  tag(id: $id){
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
        tags {
          slug
        }
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