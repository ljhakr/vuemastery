<template>
  <p>Register for the event here</p>
  <button @click="register">Register Me</button>
</template>

<script>
export default {
  data(){
    return {
    };
  },
  props: {
    event: Object,
  },
  methods: {
    register(){
      //Call to API
      //If registered then redirect to event details

      this.$router.push({
        name: 'EventDetails',
      });

      console.log('... $router.push' + ' register > event detail')
    },
  },
};
</script>
