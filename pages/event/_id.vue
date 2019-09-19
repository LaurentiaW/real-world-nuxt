<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event #' + this.event.title
        }
      ]
    }
  },
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        'http://localhost:3000/events/' + params.id
      )
      return {
        // this is now added to the data thus the computed property is now redunded
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to show info on event #' + params.id
      })
    }
  }
  // computed: {
  //   id() {
  //     return this.$route.params.id
  //   }
  // }
}
</script>
