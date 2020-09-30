<template>
    <Layout>
      <div>
        <div>
          <g-link to="/" class="article-single__home-button">
            All Articles
          </g-link>
        </div>
        <div class="article-single" :data-kontent-item-id="$page.article.id">
          <div class="article-single__inner">
            <h1 class="article-single__title" data-kontent-element-codename="title">{{$page.article.title}}</h1>
            <div
              data-kontent-element-codename="content"
              class="article-single__body"
              >
              <RichText :html="$page.article.content"></RichText>
            </div>
          </div>
          <div class="article-single__date" data-kontent-element-codename="date">
            <em>
              Published {{ $page.article.date1 | moment }}
            </em>
          </div>
          <div class="article-single__footer">
            <div class="article-single__tags">
              <ul class="article-single__tags-list" data-kontent-element-codename="tags">
                <li class="article-single__tags-list-item" v-for="tag in $page.article.tags" v-bind:key="tag.slug">
                  <g-link :to="`/tags/${tag.slug}`" class="article-single__tags-list-item-link">
                    {{tag.title}}
                  </g-link>
                </li>
              </ul>
            </div>
            <hr />
            <p class="article-single__footer-text">
              {{$page.allSiteMetadata.edges[0].node.subtitle}}
              <a
                :href="`https://twitter.com/${$page.allAuthor.edges[0].node.twitter}`"
                target="_blank"
                rel="noopener noreferrer"
              >
                <br /> <strong>{{$page.allAuthor.edges[0].node.name1}}</strong> on Twitter
                </a>
            </p>
          </div>
        </div>
      </div>
    </Layout>
</template>

<page-query>
query MyQuery($id: ID!) {
  article(id: $id) {
    title
    date1
    description
    content
    category {
      title
      slug
    }
    tags {
      title
      slug
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

import moment from 'moment';
import RichText from '../components/rich-text/richtext.vue';

export default {
  metaInfo() {
    return {
      title: `${this.$page.article.title} - ${this.$page.allSiteMetadata.edges[0].node.title}`,
      meta: [
        {
          name: 'description',
          content: `${this.$page.article.description}`
        }
      ]
    }
  },
  components: {
    RichText
  },
  filters: {
    moment: function (date) {
      return moment(date).format('D MMM YYYY');
    }
  }
}
</script>