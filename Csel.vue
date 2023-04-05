<template>
 <!-- . . . . . . . . . . . . . . . . . . .  . . . .  --> 
<p class="bg-dark p-1">
<span class="text-white navbar-brand">{{conff.f}}</span><span>&nbsp;&nbsp;&nbsp;</span>
<span class="text-white">{{conff.g}}</span><span>&nbsp;&nbsp;</span>
 <span class=""><a class="dropbtnII" @click="showTra=!showTra" v-show="isMob==true">Translate </a>
            <div class="dropdownII-content" v-if="showTra">
            <a class="nav-link"  @click="changeOne('en')" >English</a>
            <a class="nav-link" @click="googleTranslateElementInit()">Other Idioms</a>
            <a class="nav-link"  @click="changeOne('br')">Show Original</a>
            </div>
  </span>   
        <span class="dropdownIII" v-show="isMob==false">
            <a class="dropbtnIII">Translate</a>
            <div class="dropdownIII-content">
            <a @click="changeOne('en')">English</a>
            <a @click="googleTranslateElementInit()">Other Idioms</a>
            <a  @click="changeOne('br')">Show Original</a>
            </div>
          
        </span> 
</p>

<!-- . . . . . . . . . . . . . . . . . . .  . . . .  --> 
 <span v-if="traCP"><div id="gootrael"></div></span>

<div class="container-fluid  mt-4">  
<div class="container bg-white col-md-12 ">
<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
<AvalComp :msg="conff.d" :lnk="conff.e" />

<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
 <div class="container d-flex justify-content-center">
  <table border="0" class="table-primary"><tr><td> <button class="btn sideblock" @click="moveItt('left')">&#8882;</button></td>
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
  <div v-if="isActive" class="container d-flex col-md-8">
  <table border="1" class="table-primary"><tr><td>
    {{conff.a}}:  {{itt.name}}<br>
   {{conff.b}}:   {{itt.description}}<br>
    {{conff.c}}:  {{itt.development}} <br>
    </td></tr></table>
  </div>
  <br>
<!-- . . . . . . . . . . . . . . . . . . .  . . . .  -->
<div id="tabela"></div><div id="table"></div>
  <div class="container col-md-9">
  <table class="table-primary" border="1">
  <thead>
  <tr>
      <th scope="col">{{conff.a}}</th>
      <th scope="col">{{conff.b}}</th>
  </tr>
  </thead>
  <tbody>
  <tr v-for="mytt in realPro" :key="mytt.idd">
    <td>{{ mytt.name }}</td>
    <td>{{ mytt.description }}</td>
   </tr>
   </tbody>
  </table>
  </div>
 
</div>  
</div> 
  
  
</template>
<script>
 /* eslint-disable */
import prj from '@/proone.json';
import prjII from '@/proone2.json';



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
            showTra:false,
            showTray:false,
            proActive:1,
            isActive: false,
            isMob:false,
            actOne:true, 
            actTwo:false,
            traCP:false,
            conff:configvar[1]
            
        }  
    },
    computed:{     
        mybase(){
           // return prj;
           return this.projes;
        },
        realPro(){
            //this.moveItt('left');
            //console.log("------");
            //console.log(prj);
             if (this.proActive==1) {  return prj; }
            else{  return prjII; } 
        }
    },
    methods:{
    googleTranslateElementInit(){
    this.traCP=!this.traCP;
    new google.translate.TranslateElement({pageLanguage: 'en'}, 'gootrael');
    },
    detectMob() {
            const toMatch = [
                /Android/i,
                /webOS/i,
                /iPhone/i,
                /iPad/i,
                /iPod/i,
                /BlackBerry/i,
                /Windows Phone/i
            ];
            
            return toMatch.some((toMatchItem) => {
                return navigator.userAgent.match(toMatchItem);
            });
        },
   
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
            this.showTra=!this.showTra;
            this.proActive=2;
            this.moveItt('left');
            this.conff=configvar[0];
                
                
        }
         if (lg=='br'){
            this.showTra=!this.showTra;
            this.proActive=1;
            this.moveItt('left');
            this.conff=configvar[1];
        }
       
    }

  },
  mounted(){

    if (this.detectMob()==false){
        this.isMob=false;
    } else{
        this.isMob=true;
    }
    this.showItt(this.projes[0]);
    //console.log(this.isMob);
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
        height: 9rem; 
        width: 7rem;
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
        height:5rem;
        width: 3rem;
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
/* - - - - - - - - - - - - - - - - - - - */
/* - - - - - - - - - - - - - - - - - - - */
/* - - - - - - - - - - - - - - - - - - - */
/* - - - - - - - - - - - - - - - - - - - */
.dropbtnII {
    border: none;
    cursor: pointer;
    text-decoration:none;
    color:#beeaf7;
}
.dropdownII {
  position: relative;
  display: inline-block;
  text-decoration:none;
}
/* - - - - - - - - - - - - - - - - - - - */
.dropbtnIII {
    border: none;
    cursor: pointer;
    text-decoration:none;
    color:#beeaf7;
}
.dropdownIII {
  position: relative;
  display: inline-block;
  text-decoration:none;
}


/* - - - - - - - - - - - - - - - - - - - */
.dropdownIII-content {
    cursor: pointer;
  display: none;
  position: absolute;
  z-index: 1;
}
.dropdownIII-content a {
  background-color:#EFEFEF;
  color:#064f9e;
  padding: 10px 13px;
  text-decoration: none;
  display: block;
}
.dropdownIII-content a:hover{
    background-color:#15f2e7;
    color:#064f9e;
}
/* - - - - - - - - - - - - - - - - - - - */
/* Dropdown Content (Hidden by Default) */
.dropdownII-content {
  display: inline;
  position: absolute;
  z-index: 1;
}
/* Links inside the dropdown */
.dropdownII-content a {
  background-color:#EFEFEF;
  color:#064f9e;
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
.dropdownIII:hover .dropdownIII-content {
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
