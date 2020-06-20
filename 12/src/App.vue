<template>
  <div id="app">
    <Contacts></Contacts>
  </div>
</template>

<script>
  import Contacts from './components/Contacts.vue';
  export default {
    name: 'App',
    components: {
      Contacts: Contacts,
    },
    data() {
      return {};
    },
  };

</script>
