<template>
  <h1>Events to make the world better</h1>
  <div class="event">
    <EventCard
        v-for="event in events"
        :key="event.id"
        :event="event"
    />

    <div class="pagination">
      <router-link
          :to="{name: 'EventList', query: {page: page-1}}"
          rel="Prev"
          class="previous"
          v-if="page !== 1">
        &#60; Previous
      </router-link>
      <router-link
          :to="{name: 'EventList', query: {page: page+1}}"
          rel="Next"
          class="next"
          v-if="hasNextPage">
        Next &#62;
      </router-link>
    </div>

  </div>
</template>
<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue';
import EventService from '@/services/EventService';
import { watchEffect } from 'vue';

export default {
  name: 'EventList',
  props: ['page'],
  components: {
    EventCard,
  },
  data() {
    return {
      events: null,
      totalEvents: 0,
    };
  },
  created() {
    watchEffect(() => {
      this.events = null;
      EventService.getEvents(2, this.page)
      .then(response => {
        this.events = response.data;
        this.totalEvents = response.headers['x-total-count'];
      }).catch(() => {
        this.$router.push({ name: 'NetworkError' })
      });
    })
  },
  computed: {
    hasNextPage(){
      var totalPages = Math.ceil(this.totalEvents / 2);
      return this.page < totalPages;
    },
  },
};
</script>

<style>
.event {
  align-items: center;
  display: flex;
  flex-direction: column;
}
.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
}

.pagination .previous {
  text-align: left;
}

.pagination .next {
  text-align: right;
}
</style>
