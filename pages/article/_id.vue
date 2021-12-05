<template>
  <div>
    <client-only>
      <h1>{{ item.title }}</h1>
      <p v-html="$md.render(item.body)"></p>
      <NuxtLink to="/">戻る</NuxtLink>
    </client-only>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      item: [],
    }
  },
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://engineerblog.microcms.io/api/v1/blog-posting/${params.id}`,
      {
        headers: { 'X-MICROCMS-API-KEY': process.env.API_KEY },
      }
    )
    return {
      item: data,
    }
  },
}
</script>
