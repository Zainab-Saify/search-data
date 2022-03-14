<template>
 <v-app>
   <cusdata></cusdata>
</v-app>
</template>

<script>
import cusdata from '../src/views/data.vue'

export default {
  
  name: 'App',

  components:{
    cusdata
  },

  data: () => ({
    //
  }),
};
</script>
