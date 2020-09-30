<template>
    <div class="sidebar">
      <div class="sidebar__inner">
        <div class="sidebar__author" :data-kontent-item-id="$static.allAuthor.edges[0].node.id">
          <div>
            <a href="/">
              <img
                :src="$static.allAuthor.edges[0].node.avatarImage[0].url"
                class="sidebar__author-photo"
                width="75"
                height="75"
                :alt="$static.allAuthor.edges[0].node.name1"
                data-kontent-element-codename="avatar_image"
              />
            </a>
            <h1 v-if="isHomePage" class="sidebar__author-title" data-kontent-element-codename="name">
                <a class="sidebar__author-title-link" to="/">
                  {{$static.allAuthor.edges[0].node.name1}}
                </a>
            </h1>
            <h2 v-else class="sidebar__author-title" data-kontent-element-codename="name">
                <a class="sidebar__author-title-link" to="/">
                  {{$static.allAuthor.edges[0].node.name1}}
                </a>
            </h2>
            <p class="sidebar__author-subtitle" data-kontent-element-codename="bio">
                {{$static.allAuthor.edges[0].node.bio}}
            </p>
          </div>
        </div>
        <div>
          <Menu />
          <Links />
          <p class="sidebar__copyright">{{$static.allSiteMetadata.edges[0].node.copyright}}</p>
        </div>
      </div>
    </div>
</template>

<script>
import Menu from "~/components/menu.vue"
import Links from "~/components/links.vue"

export default {
    components: {
      Menu,
      Links
    },
    props: {
        isHomePage: Boolean,
        routeParams: Object
    }
}
</script>

<static-query>
query MyQuery {
  allAuthor(filter: { codename: { eq: "author" } }) {
    edges {
      node {
        id
        codename
        name1
        avatarImage {
          url
        }
        bio
      }
    }
  }
  allSiteMetadata(limit: 1) {
    edges{
      node{
        copyright
      }
    }
  }
}

</static-query>