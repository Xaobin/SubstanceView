<template>
<div class="container col-md-9">
   <small class="mt-3 float-none"> {{conf.l}}</small><hr>
  <table class="ytable ybordered text-black" border="0">
  <thead>
  <tr>
      <th scope="col">{{conf.a}}</th>
      <th scope="col">{{conf.b}}</th>
  </tr>
  </thead>
  <tbody>
  <tr v-for="mytt in realpro" :key="mytt.idd">
    <td>{{ mytt.name }}</td>
    <td>{{ mytt.description }}</td>
   </tr>
   </tbody>
  </table>
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
     realpro: {},
     conf:{}
   }, 
   name: 'TableComp',
   components: {
    
  },
    
    methods:{
    
  },
  mounted(){
     
  }

}

</script>
<style scoped>
.ytable,.ytable-all{border-collapse:collapse;border-spacing:0;width:100%;display:table}.ytable-all{border:1px solid #ccc}
.ybordered tr,.ytable-all tr{border-bottom:1px solid #c1c1c1}.ystriped tbody tr:nth-child(even){background-color:#f1f1f1}
.ytable-all tr:nth-child(odd){background-color:#fff}.ytable-all tr:nth-child(even){background-color:#f1f1f1}
.yhoverable tbody tr:hover,.yul.yhoverable li:hover{background-color:#ccc}.ycentered tr th,.ycentered tr td{text-align:center}
.ytable td,.ytable th,.ytable-all td,.ytable-all th{padding:8px 8px;display:table-cell;text-align:left;vertical-align:top}
.ytable th:first-child,.ytable td:first-child,.ytable-all th:first-child,.ytable-all td:first-child{padding-left:16px}

</style>
