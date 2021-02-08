<template>
  <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
  <p>{{ event.description }}</p>
</template>

<script>
export default {
  data(){
    return{
      clickCounter: 100,
    }
  },
  props: ['event']
}
</script>
