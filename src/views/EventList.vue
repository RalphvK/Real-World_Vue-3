<template>
  <div class="events">
    <h1>Events For Good</h1>
    <div class="event-list" v-if="events">
      <EventCard v-for="event in events" :key="event.id" :event="event" />
    </div>
    <BaseLoader v-show="loading" />
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'
import BaseLoader from '@/components/BaseLoader.vue'

export default {
  name: 'Home',
  components: {
    EventCard,
    BaseLoader
  },
  data() {
    return {
      loading: false,
      events: null
    }
  },
  created() {
    this.loading = true
    EventService.getEvents()
      .then(response => {
        this.events = response.data
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

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
