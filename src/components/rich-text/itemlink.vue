<template>
  <g-link :to="node.path">
    <slot />
  </g-link>
</template>

<script>
export default {
  props: {
    node: {
      type: Object,
      required: true
    }
  }
};
</script>