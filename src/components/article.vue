<template>
    <div class="article" :data-kontent-item-id="article.id">
        <div class="article__meta">
          <time
            class="article__meta-time"
            :dateTime="article.date"
            data-kontent-element-codename="date"
          >
            {{ article.date1 | moment }}
          </time>
          <span class="article__meta-divider" />
          <span class="article__meta-category" :key="article.category.slug" data-kontent-element-codename="category">
              <g-link :to="`/categories/${article.category[0].slug}`" class="article__meta-category-link">{{article.category[0].title}}</g-link>
          </span>
        </div>
        <h2 class="article__title" data-kontent-element-codename="title">
          <g-link :to="`${article.path}`" class="article__title-link">{{article.title}}</g-link>
        </h2>
        <p class="article__description" data-kontent-element-codename="description">{{article.description}}</p>
        <g-link class="article__readmore" :to="article.path">Read</g-link>
    </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
      article: Object,
  },
  filters: {
    moment: function (date) {
      return moment(date).format('MMMM YYYY');
    }
  }
}
</script>