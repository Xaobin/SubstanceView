<template>
<div class="container col-md-6">
<span><a href="https://github.com/Xaobin" target="_blank"><small class="smll">{{per}}</small></a></span>
<span>&nbsp;&nbsp;&nbsp;<div class="arrow-up ml-2"></div></span>
<div class="alert alert-info alert-dismissible fade show" v-if="inShow">

    {{msg}} <a :href="'#'+lnk">{{lnk}}</a>
    
</div>
</div>
</template>
<script>
/* eslint-disable */
  export default {
  data(){
        return {
        inShow:true
   }},     
   props: {
     msg: String,
     lnk:String,
     per:String
   }, 
   name: 'AvalComp',
   components: {
    
  },
    
    methods:{
    
  },
  mounted(){
     
  }

}

</script>
<style scoped>
.arrow-up {
  width: 0; 
  height: 0; 
  border-left: 15px solid transparent;
  border-right: 15px solid transparent;
  
  border-bottom: 15px solid #D6EBFD;
}
.smll{
color:black;
font-size:10px;
text-decoration:underline;
}

</style>
