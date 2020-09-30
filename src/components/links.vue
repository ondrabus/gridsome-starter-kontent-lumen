import React from 'react'
import './style.scss'
import '../../assets/fonts/fontello-771c82e0/css/fontello.css'

class Links extends React.Component {
  render() {
    const author = this.props.data
    const links = {
      telegram: author.elements.telegram.value,
      twitter: author.elements.twitter.value,
      github: author.elements.github.value,
      vk: author.elements.vk.value,
      // rss: author.elements.rss.value,
      email: author.elements.email.value,
    }

    return (
      
    )
  }
}

<template>
    <div class="links">
        <ul class="links__list">
          <li v-if="$static.allAuthor.edges[0].node.twitter != ''" class="links__list-item" data-kontent-element-codename="twitter">
            <a
              :href="`https://www.twitter.com/${$static.allAuthor.edges[0].node.twitter}`"
              target="_blank"
              rel="noopener noreferrer"
            >
              <i class="icon-twitter" />
            </a>
          </li>
          <li v-if="$static.allAuthor.edges[0].node.github != ''" class="links__list-item" data-kontent-element-codename="github">
            <a
              :href="`https://www.github.com/${$static.allAuthor.edges[0].node.github}`"
              target="_blank"
              rel="noopener noreferrer"
            >
              <i class="icon-github" />
            </a>
          </li>
          <li v-if="$static.allAuthor.edges[0].node.vk != ''" class="links__list-item" data-kontent-element-codename="vk">
            <a
              :href="`https://www.vk.com/${$static.allAuthor.edges[0].node.vk}`"
              target="_blank"
              rel="noopener noreferrer"
            >
              <i class="icon-vkontakte" />
            </a>
          </li>
          <li v-if="$static.allAuthor.edges[0].node.email != ''" class="links__list-item" data-kontent-element-codename="email">
            <a :href="`mailto:${$static.allAuthor.edges[0].node.email}`">
              <i class="icon-mail" />
            </a>
          </li>
          <li v-if="$static.allAuthor.edges[0].node.telegram != ''" class="links__list-item" data-kontent-element-codename="telegram">
            <a :href="`telegram:${$static.allAuthor.edges[0].node.telegram}`">
              <i class="icon-paper-plane" />
            </a>
          </li>
        </ul>
      </div>
</template>

<static-query>
query MyQuery {
  allAuthor(filter: { codename: { eq: "author" } }) {
    edges {
      node {
        twitter
        github
        vk
        email
        telegram
      }
    }
  }
}
</static-query>