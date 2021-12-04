<template>
  <div>
    <p>{{ $route.params.id }}</p>
    <NuxtLink to="/">戻る</NuxtLink>
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
    async asyncData({ params }) {
      const { data } = await axios.get(
        `https://engineerblog.microcms.io/api/v1/blog-posting/${params.id}`,
        {
          headers: { 'X-MICROCMS-API-KEY': process.env.API_KEY },
        }
      )
      return {
        items: data,
      }
    },
}
</script>
