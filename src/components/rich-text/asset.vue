<template>
  <figure><v-lazy-image
    :src="node.url"
    :src-placeholder="node.placeholderUrl"
    :alt="node.description"
  /></figure>
</template>

<script>
import VLazyImage from 'v-lazy-image';

export default {
  components: {
    VLazyImage
  },
  props: {
    node: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
img {
   width: 100%;
}

.v-lazy-image {
  filter: blur(5px);
  transition: filter 1.6s;
  will-change: filter;
}

.v-lazy-image-loaded {
  filter: blur(0);
}
</style>