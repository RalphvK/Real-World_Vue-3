<template>
  <div>
    <h1>{{ event.title }}</h1>
    <p>{{ event.title }} is on {{ event.date }} @ {{ event.location }}</p>
  </div>
</template>

<script>
import EventService from '@/services/EventService'

export default {
  props: {
    id: [String, Number]
  },
  data() {
    return {
      event: {}
    }
  },
  created() {
    EventService.getEvent(this.id)
      .then(response => {
        this.event = response.data
      })
      .catch(error => {
        alert(error)
      })
  }
}
</script>
