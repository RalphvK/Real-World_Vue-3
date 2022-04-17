<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.title }} is on {{ event.date }} @ {{ event.location }}</p>
  </div>
  <BaseLoader v-show="loading" />
</template>

<script>
import EventService from '@/services/EventService'
import BaseLoader from '@/components/BaseLoader.vue'

export default {
  components: {
    BaseLoader
  },
  props: {
    id: [String, Number]
  },
  data() {
    return {
      event: null,
      loading: false
    }
  },
  created() {
    this.loading = true
    EventService.getEvent(this.id)
      .then(response => {
        this.event = response.data
      })
      .catch(error => {
        alert(error)
      })
      .then(() => {
        this.loading = false
      })
  }
}
</script>
