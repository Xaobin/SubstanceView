<template>
  <div class="w3-container">
  

 <div class="centerblock">
  <table border="0"><tr><td> <button class="sideblock" @click="moveItt('left')">Left Side</button></td>
  <span v-if="actOne">
  <span v-for="item in mybase" :key="item.idd">
    <td v-if="item.visible==true"><button class="w3-button retblock" @click="showItt(item)">{{ item.name }}</button></td>
   </span>
   </span>
   <td><button class="sideblock" @click="moveItt('right')">Right Side</button></td>
  </tr></table>
</div> 
   
   
  <br>
  <div v-if="isActive">
    Name: {{itt.name}}<br>
   Descript:  {{itt.description}}<br>
    Dev: {{itt.development}} <br>
  </div>
  <br>
 
  
 
  
  </div>
</template>
<script>
import prj from '@/proone.json'
  export default {
  /* eslint-disable */
   name: 'CselComp',
 //  props: { items: {} },
    data(){
        return {
            itt:{},
            isActive: false,
            actOne:true
            
        }  
    },
    computed:{     
        mybase(){
            return prj;
        }
    },
    methods:{
     showItt(item){
        this.itt=item;
        this.isActive=true;
       // console.log(this.itt);
    },
    moveItt(tmov){
        let projs=prj;
        let signal=false;
        let idex=-1;
        this.actOne=false;
        projs.forEach(jobj => {
            Object.entries(jobj).forEach(([khey, vall]) => {
                if (khey=="idd"){ idex++; }
                if (tmov=="right"){
                if ((khey=="visible")&&(vall==true)&&(signal==false)){
                 if ((projs[idex].visible!=undefined)&&(projs[idex+2]!=undefined)){
                     projs[idex].visible=false;
                     projs[idex+2].visible=true;   
                     signal=true;
                 }
                 
                }
                }
                if (tmov=="left"){
                 if ((khey=="visible")&&(vall==true)&&(signal==false)){
                 if ((projs[idex+1]!=undefined)&&(projs[idex-1]!=undefined)){ 
                     projs[idex-1].visible=true;
                      projs[idex+1].visible=false;
                      signal=true;   
                      
                }
                }    
                }
                
         });
        });
        prj=projs;
        this.actOne=true;
        //console.log(this.mybase);
        //this.mybase;
    
    }

  },
  mounted(){
  
   //this.mybase();
   //console.log("Csel");
  // console.log(this.mybase);
  }

}

</script>

<style scoped>
    .centerblock{
    
        width: 50%;
        border: 1px solid;
        margin: auto;
        flex-direction: column;
    }
    .pdd { 
        padding-top:0rem;
        padding-bottom: 0rem;
        padding-right: 2rem;
        padding-left: 0rem;
        float:left;
        width:13.33333%
    }
    .retblock{
        height: 20rem; 
        width: 10rem;
        flex-direction: column;
        background-color:#0095df;
        color:#ebecee;
        /*margin: 0 auto;*/
        display:inline-block;
        padding-right: 0rem;
        padding-left: 0rem;
            
    }
    .sideblock{
        height:17rem;
        width: 4rem;
        background-color:#0095df;
        color:#ebecee;
        /*margin: 0 auto;*/
        /*display:inline-block;*/
      
    }
    .liner{
        display: inline;
    }
    .fontwhite{
        color:#ebecee;
    }

    .centralize {
    margin: auto;
    width: 150%;
    border: 0px ;
    padding: 2px;
    }

  
</style>
