<template>
    <nav class="menu">
        <ul class="menu__list">
          <li v-for="menuItem in $static.allMenu.edges[0].node.menuItems" class="menu__list-item" :key="menuItem.id">
            <g-link :to="menuItem.slug" class="menu__list-item-link">{{menuItem.label}}</g-link>
          </li>
        </ul>
    </nav>
</template>

<static-query>
query MyQuery {
  allMenu (filter:{codename:{eq:"navigation_menu"}}){
    edges
    {
      node{
        menuItems {
          id
          label
          slug
        }
      }
    }
  }
}
</static-query>

<script>
export default {
    props: {
        routeParams: Object
    }
}
</script>
