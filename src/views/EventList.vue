<template>
  <h1>Events to make the world better</h1>
  <div class="event">
    <EventCard
        v-for="event in events"
        :key="event.id"
        :event="event"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue';
import EventService from '@/services/EventService';

export default {
  name: 'EventList',
  components: {
    EventCard,
  },
  data() {
    return {
      events: null,
    };
  },
  created() {
    EventService.getEvents().then(response => {
      this.events = response.data;
    }).catch(error => {
      console.log(error);
    });
  },
};
</script>

<style>
.event {
  align-items: center;
  display: flex;
  flex-direction: column;
}
</style>
