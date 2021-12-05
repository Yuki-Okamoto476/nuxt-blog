<template>
  <div>
    <h1>test-blog</h1>
    <div v-for="(item, key) in items" :key="key">
      <nuxt-link :to="'article/' + item.id">
        <h2>{{ item.title }}</h2>
      </nuxt-link>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      items: [],
    }
  },
  async asyncData({ error }) {
    try {
      const { data } = await axios.get(
        'https://engineerblog.microcms.io/api/v1/blog-posting',
        {
          headers: { 'X-MICROCMS-API-KEY': process.env.API_KEY },
        }
      )
      return {
        items: data.contents,
      }
    } catch (err) {
      error({
        statusCode: err.response.status,
        message: err.response.data.message,
      })
    }
  },
}
</script>
