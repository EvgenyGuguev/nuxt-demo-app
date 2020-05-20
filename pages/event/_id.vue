<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        'http://localhost:3030/events/' + params.id
      )
      return {
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: `Unable to fetch event #${params.id} at this time. Please try again.`
      })
    }
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'My description for ' + this.event.title
        }
      ]
    }
  }
}
</script>

<style scoped></style>
