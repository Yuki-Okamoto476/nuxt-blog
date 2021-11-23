<template>
  <div>
    <h1>test-blog</h1>
    <div v-for="(item,key) in items" :key="key">
       <h2>{{ item.title }}</h2>
       <p>{{ item.body }}</p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      items: []
    };
  },
  async asyncData() {
    const { data } = await axios.get(
      "https://engineerblog.microcms.io/api/v1/blog-posting",
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY }
      }
    );
    return {
      items: data.contents
    };
  }
}
</script>

