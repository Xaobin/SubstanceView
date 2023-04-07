<template>
<div>
<!-- The Modal -->
<div :id="modalname" class="ymodal" v-on:click="vvvNoMouse()">
  <div class="ymodal-content" @mouseover="mousein='true'"
    @mouseout="mousein='false'">
    <div class="container">
        <span @click="vvvNoShow()" class="yclose">&times;</span>
        <h5 class="modal-title" :id="modalname">{{title}}</h5>
        <hr>
      <span v-show="((isMob==true)||(isMob=='true'))"><img :src="mimage" width="300" height="300"></span>
      <span v-show="((isMob==false)||(isMob=='false'))"><img :src="mimage" width="600" height="600"></span>
       <slot name="alerts"></slot>  
        <div id="conntt" @click="mousein='true'">
            <slot name="content"></slot>
        </div> 
    </div>
        <button class="btn btn-secondary" @click="vvvNoShow()">Close</button>
        <slot name="footer"></slot>
  </div>
</div>





   
</div>
</template>
<script>

export default {
/* eslint-disable */
    name:'DModalComp',
     props: {
     title: String,
     modalname:String,
     mimage:String,
     isMob:[Boolean, String]
   }, 
     data() {
            return {
                mousein:'true', 
                mousecon:'true'
        }},
     methods:{
         vvvNoShow(){
            let name=this.modalname;
            document.getElementById(name).style.display='none';
            
        },
        vvvNoMouse(){
            if ((this.mousein=='false')){
               this.vvvNoShow();
            }
        },
        
     }
    
}    

</script>
<style scoped>
.ymodal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.9); /* Black w/ opacity */
}

/* Modal Content (Image) */
.ymodal-content {
  margin: auto;
  display: block;
  width: 80%;
  max-width: 700px;
}

/* Caption of Modal Image (Image Text) - Same Width as the Image */
#ycaption {
  margin: auto;
  display: block;
  width: 80%;
  max-width: 700px;
  text-align: center;
  color: #ccc;
  padding: 10px 0;
  height: 150px;
}

/* Add Animation - Zoom in the Modal */
.ymodal-content, #caption {
  animation-name: zoom;
  animation-duration: 0.6s;
}

@keyframes zoom {
  from {transform:scale(0)}
  to {transform:scale(1)}
}

/* The Close Button */
.yclose {
  position: absolute;
  top: 15px;
  right: 35px;
  color: #f1f1f1;
  font-size: 40px;
  font-weight: bold;
  transition: 0.3s;
}

.yclose:hover,
.yclose:focus {
  color: #bbb;
  text-decoration: none;
  cursor: pointer;
}

/* 100% Image Width on Smaller Screens */
@media only screen and (max-width: 700px){
  .ymodal-content {
    width: 100%;
  }
}
</style>
