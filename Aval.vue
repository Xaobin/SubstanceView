<template>
  <div>
    
    
    <CselComp />
   
  </div>
</template>
<script>
/* eslint-disable */
import dtt from '@/lang.json'
import CselComp from '@/components/Csel.vue'
  export default {
  
   name: 'AvalComp',
   components: {
    CselComp
  },
    
    methods:{
    
  },
  mounted(){
     console.log(dtt[0].a);
  }

}

</script>
