<template>
  <div>
    <h1>Events</h1>
    <event-card
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '../components/EventCard'
export default {
  components: {
    EventCard
  },
  asyncData({ $axios, error }) {
    return $axios
      .get('http://localhost:3030/events')
      .then((response) => {
        return {
          events: response.data
        }
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: 'Unable to fetch events at this time. Please try again.'
        })
      })
  },
  head() {
    return {
      title: 'All Events'
    }
  }
}
</script>

<style></style>
