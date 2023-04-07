<template>
<div class="container col-md-9">
   <small class="mt-3 float-none"> {{lang.l}}</small><hr>
  <table class="ytable ybordered text-black" border="0">
  <thead>
  <tr>
      <th scope="col">{{lang.a}}</th>
      <th scope="col">{{lang.b}}</th>
  </tr>
  </thead>
  <tbody>
  <tr v-for="mytt in realpro" :key="mytt.idd">
    <td>{{ mytt.name }}</td>
    <td>{{ mytt.description }}<br>
    <strong>{{lang.c}}</strong>:  {{mytt.development}} <br>
     <span v-if="mytt.photos!='nullable'">
        <strong class="mt-1">{{lang.i}}</strong>:
        <span v-for="ity in mytt.photos" :key="ity.kk">
        <span class="col-sm"><!-- . .Images List.  -->
        <a id="myImg" class="abluelink"  @click="showMod(ity.vv)">{{lang.n}}{{ity.kk}}
        </a>&nbsp;
        </span> </span><br>
    </span>
       <span v-if="mytt.link!='nullable'">
          <strong>{{lang.j}}</strong>:
           <a :href="mytt.link" target="_blank"><button class='btn btn-sm btn-outline-primary mt-1'>{{lang.m}}</button></a>
       </span>
    </td>
   </tr>
   </tbody>
  </table>
  <DModalComp :title="lang.k" modalname="viewImageB" isMob='false' :mimage="simage" />
  </div>
</template>
 
<script>
/* eslint-disable */
import DModalComp from '@/components/DModal.vue';
  export default {
      data(){
        return {
            simage:''
           } },
            
   props: {
     realpro: {},
     lang:{}
   }, 
   name: 'TableComp',
   components: {
    DModalComp
  },
    
methods:{
    showMod(ima){
        this.simage=ima;
        document.getElementById('viewImageB').style.display='block';
    },
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

.abluelink{color:#349bef; text-decoration:underline;}
 #myImg {
        border-radius: 5px;
        cursor: pointer;
        transition: 0.3s;
    }
    #myImg:hover {opacity: 0.7;}
</style>
