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
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'
// now making use of VUEX and not calling from EventService but from the store
// import EventService from '@/services/EventService.js'

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
  // async asyncData({ $axios, error }) {

  // remove $axios when using the EventService
  // async asyncData({ error }) {

  // using vuex thus not asyncData but fetch  and add the store to the arguments
  async fetch({ store, error }) {
    try {
      // const { data } = await $axios.get('http://localhost:3000/events')
      // adding the event service thus this syntax gets updated to incl this rather than making the call it self
      //   const { data } = await EventService.getEvents()
      //   return {
      //     events: data
      //   }
      // }

      // for vuex remove the returned values and call store dispatch events, fetchEvents
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to show events at this time. Please try again.'
      })
    }
  },
  // for Vuex add computed property use mapState to map the Events property
  computed: mapState({
    events: (state) => state.events.events
  })
}
</script>
