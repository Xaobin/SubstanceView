<template>
  

  <nav class="navbar navbar-expand-md py-md-0 navbar-dark bg-dark">
<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
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
            <a class="nav-link" href="#" @click="changeOne('en')">English</a>
            <a class="nav-link" href="#">Other Idioms</a>
            <a class="nav-link" href="#" @click="changeOne('br')">Show Original</a>
            </div>
          
        </li>  
      </ul>
      
    </div>
  </div>
</nav>


<div class="container-fluid  mt-4">  
<div class="container bg-white col-md-12 ">

<AvalComp msg="Obrigado por comparecer a este portfólio, logo abaixo encontra-se a lista de projetos realizados, para acessá-los basta navegar por meio dos botões anteior e posterior, caso queira a lista completa dos projetos acesse" lnk="#t1" />

<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
 <div class="centerblock">
  <table border="0"><tr><td> <button class="btn sideblock" @click="moveItt('left')">&#8882;</button></td>
  <span v-if="actOne">
  <span v-for="item in mybase" :key="item.idd">
    <td v-if="item.visible==true"><button class="btn retblock" @click="showItt(item)">{{ item.name }}</button></td>
   </span>
   </span>
   <td><button class="btn sideblock" @click="moveItt('right')">&#8883;</button></td>
  </tr></table>
</div> 
   
<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->   
  <br>
  <div v-if="isActive">
    Name: {{itt.name}}<br>
   Descript:  {{itt.description}}<br>
    Dev: {{itt.development}} <br>
  </div>
  <br>
<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
  <div class="container col-md-9 ">
  <table class="table table table-striped">
  <tr>
      <th scope="col">{{conff.a}}</th>
      <th scope="col">{{conff.b}}</th>
  </tr>
  <tr v-for="mytt in realPro" :key="mytt.idd">
    <td>{{ mytt.name }}</td>
    <td>{{ mytt.description }}</td>
   </tr>
  </table>
  </div>
 
</div>  
</div> 
  
  
</template>
<script>
 /* eslint-disable */
import prj from '@/proone.json';
import prjII from '@/proone.json';



import AvalComp from '@/components/Aval.vue';
import configvar from '@/confs.json';

  export default {
 
   name: 'CselComp',
 //  props: { items: {} },
    components: {
        AvalComp
    },
    data(){
        return {
            itt:{},
            projes:prj,
            
            proActive:1,
            isActive: false,
            actOne:true, 
            actTwo:false,
            conff:configvar[1]
            
        }  
    },
    computed:{     
        mybase(){
           // return prj;
           return this.projes;
        },
        realPro(){
            //console.log("------");
            //console.log(prj);
             if (this.proActive==1) {  return prj; }
            else{  return prjII; } 
        }
    },
    methods:{
     showItt(item){
        this.itt=item;
        this.isActive=true;
       // console.log(this.itt);
    },
    moveItt(tmov){
      if (this.proActive==1) { this.projes=prj; }
      else{ this.projes=prjII; } 
        let projs=this.projes;
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
        this.projes=projs;
        this.actOne=true;
        //console.log(this.mybase[0].name);
        //this.mybase;
    
    },
    changeOne(lg){
        
        if (lg=='en'){
            this.proActive=2;
            this.moveItt('left');
            this.conff=configvar[0];
        }
         if (lg=='br'){
            this.proActive=1;
            this.moveItt('left');
            this.conff=configvar[1];
        }
       
    }

  },
  mounted(){
    //this.prlist=prjOrig;
    //this.prlistII=prjIIOrig;
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
        height: 13rem; 
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
        height:10rem;
        width: 4rem;
        background-color:#0095df;
        color:#ebecee;
       font-size:30px;
      
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
 
  
  z-index: 1;
}

/* Links inside the dropdown */
.dropdownII-content a {
  background-color:#EFEFEF;
  color:blue;
  padding: 10px 13px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover 
.dropdown-content a:hover {background-color: #68dff2}*/

/* Show the dropdown menu on hover */
.dropdownII:hover .dropdownII-content {
  display: block;
  
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdownII:hover .dropbtnII {
  
}
    
    
    .centralize {
    margin: auto;
    width: 150%;
    border: 0px ;
    padding: 2px;
    }

  
</style>
