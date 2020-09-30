<template>
    <Layout>
      <Sidebar :isHomePage="false" :routeParams="this.$route.params" />
      <div class="content">
        <div class="content__inner">
          <div class="page" :data-kontent-item-id="$page.contentPage.id">
            <h1 class="page__title"
              data-kontent-element-codename="title">
              {{$page.contentPage.title}}
            </h1>
            <div
              class="page__body"
              data-kontent-element-codename="description"
            >
              <RichText :html="$page.contentPage.description"></RichText>
            </div>
          </div>
        </div>
      </div>
    </Layout>
</template>

<page-query>
query MyQuery($id: ID!) {
  contentPage(id: $id){
    name
    title
    metaDescription
    description
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
  allAuthor(filter: { codename: { eq: "author" } }) {
    edges {
      node {
        name1
        twitter
      }
    }
  }
}

</page-query>

<script>

import Sidebar from "~/components/sidebar.vue"
import RichText from '../components/rich-text/richtext.vue';

export default {
  metaInfo() {
    return {
      title: `${this.$page.contentPage.title} - ${this.$page.allSiteMetadata.edges[0].node.title}`,
      meta: [
        {
          name: 'description',
          content: `${this.$page.contentPage.metaDescription}`
        }
      ]
    }
  },
  components: {
    Sidebar,
    RichText
  }
}
</script>