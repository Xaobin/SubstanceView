<template>
  
  
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Portfolio</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarColor01">
      <ul class="navbar-nav me-auto">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home
            <span class="visually-hidden">(current)</span>
          </a>
        </li>
        
        <li class="nav-item">
          <a class="nav-link" href="#">About</a>
        </li>
    
        <li class="nav-link dropdownII">
            <a class="dropbtnII">Translate Page</a>
            <div class="dropdownII-content">
                <a class="text-white" href="#">Link 1</a>
                <a class="text-white" href="#">Link 2</a>
                <a class="text-white" href="#">Link 3</a>
                      <a class="nav-link" href="#">English</a>
            <a class="nav-link" href="#">Other Idioms</a>
            <a class="nav-link" href="#">Show Original</a>
            </div>
          
        </li>  
      </ul>
      
    </div>
  </div>
</nav>

  <div>
  
 <div class="centerblock">
  <table border="0"><tr><td> <button class="sideblock" @click="moveItt('left')">Left Side</button></td>
  <span v-if="actOne">
  <span v-for="item in mybase" :key="item.idd">
    <td v-if="item.visible==true"><button class="btn retblock" @click="showItt(item)">{{ item.name }}</button></td>
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
            actOne:true, 
            actTwo:false
            
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
    @import '@/assets/spacelab.css';
    .centerblock{
    
        width: 50%;
        border: 1px solid;
        margin: auto;
        /*display:table;*/
       
    }
    .pdd { 
        float:center;
        width:13.33333%
    }
    .retblock{
        height: 20rem; 
        width: 10rem;
        flex-direction: row;
        background-color:#0095df;
        color:#ebecee;
        /*display: inline-flex;table-cell
        position: absolute;
        */
       display: flex !important;
        align-items: center;
        justify-content: center;
        padding-right: 0rem;
        padding-left: 0rem;
            
    }
    .retbtn{
        background-color:#0095df;
        color:#ebecee;
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
    .menublock{
        color:#ebecee;
        background-color:#5077A1;
         width: 20%;
        border: 1px solid;
        z-index:1055;
    }

    .dropbtnII {
        color: white;
        border: none;
        cursor: pointer;
}

/* The container <div> - needed to position the dropdown content */
.dropdownII {
  position: relative;
  display: inline-block;
  text-decoration:none;
}

/* Dropdown Content (Hidden by Default) */
.dropdownII-content {
  display: none;
  position: absolute;
  background-color: #4C749F;
  color:#ebecee;
  z-index: 1;
}

/* Links inside the dropdown */
.dropdownII-content a {
  
  padding: 10px 13px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover 
.dropdown-content a:hover {background-color: #68dff2}*/

/* Show the dropdown menu on hover */
.dropdownII:hover .dropdownII-content {
  display: block;
  background-color: #4C749F;
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdownII:hover .dropbtnII {
  background-color: #4C749F;
}
    
    
    .centralize {
    margin: auto;
    width: 150%;
    border: 0px ;
    padding: 2px;
    }

  
</style>
