<template>
  <h1>Passenger</h1>
  <div class="events">
    <EventCard
      v-for="event in events.data"
      :key="event._id"
      :event="event"
    ></EventCard>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'
import { watchEffect } from '@vue/runtime-core'
export default {
  name: 'EventListView',
  props: {
    page: {
      type: Number,
      required: true
    },
    limit: {
      type: Number,
      required: true
    }
  },
  components: {
    EventCard
  },
  data() {
    return {
      events: null,
      totalEvents: 0
    }
  },
  created() {
    watchEffect(() => {
      EventService.getEvents(this.page, this.limit)
        .then((response) => {
          this.events = response.data
          this.totalEvents = response.headers['x-total-count']
          console.log(this.events.data[0].airline[0].name)
        })
        .catch((error) => {
          console.log(error)
        })
    })
  },
  computed: {
    hasNextPage() {
      let totalPages = Math.ceil(this.totalEvents / 2)
      return this.page < totalPages
    }
  }
}
</script>
<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}
#page-prev {
  text-align: left;
}
#page-next {
  text-align: right;
}
</style>
