<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'

export default {
  head() {
    return {
      title: 'Event Listing'
    }
  },
  components: {
    EventCard
  },
  // using promises with then
  // asyncData({ $axios, error }) {
  //   return $axios
  //     .get('http://localhost:3000/events')
  //     .then((response) => {
  //       return {
  //         events: response.data
  //       }
  //     })
  //     .catch((e) => {
  //       error({
  //         statusCode: 503,
  //         message: 'Unable to show events at this time. Please try again.'
  //       })
  //     })
  // }
  // using Async Await
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to show events at this time. Please try again.'
      })
    }
  }
}
</script>
