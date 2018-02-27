<template>
<div>


  <div class="container">

      <header class="header"><h1  class="h1">Weather App</h1></header>
     <div class="row">
       <input type="text" id="place" v-model.trim="enter" class="inp" placeholder="City name" required>
       <label for="place" class="label-primary">City name</label>
     <button @click="find" class="btn" :disabled="enter.length <= 0">Show Weather</button>
     </div>

     <div class="row1" v-if="see">
        <div v-if="spin">
             <app-spinner></app-spinner>
        </div>
      <label class="label" v-if="error">{{ ' Try to enter Correct Cityname '}} </label>
           <ul v-for="d in data" class="ull" :key="d+1" v-else>
           <li class="lii" >Place : {{d.name}}  </li>
           <li class="lii"  >Temperature : {{d.temp+'°'}} C</li>
           <li class="lii" >Description : {{d.des}} </li> 
              
       </ul>
     </div>
     
  </div>
  <footer class="footer">
      <h1 class="footer__h1">Saigowtham</h1>
  </footer>
 </div>
</template>


<script>
import Spinner from './Spinner.vue';
export default {
  data(){
      return{
       enter:'',
       data:[],
       see:false,
       spin:false,
       error:false,
       
       
      }
  },

  methods:{
      find(){
          this.data=[];
          this.error=false;
          this.see=true;
          this.spin=true;
           var apikey='your api key';
           var url='https://api.openweathermap.org/data/2.5/weather?q='+this.enter+'&units=metric&appid='+apikey;
          this.$http.get(url)
          .then(response=>{
              if(this.enter.length >1){
              return response.json()
              }
          }).then(data=>{
              
              this.spin=false;
             this.error=false;
             
              var data1=[];
              var obj={
                  name:data.name,
                  temp:data.main.temp,
                  des:data.weather[0].description,
              }
           
             if(data1.length === 0){
                 data1.push(obj)
                 this.data=data1
              }   

          }).catch(error=>{
              this.spin= false;
              this.error=true
           
          })
      }
     
    
  },
 


  components:{
      'app-spinner':Spinner
  }

}
</script>

<style lang="css" scoped>


html{
    font-size: 62.5%;
   
    
}
 .container{
     
  
     
      background-image:linear-gradient(to right bottom , 
      rgba(142, 149, 248, 0.596)
      ,rgba(0, 128, 0, 0.5)),url(https://static.vecteezy.com/system/resources/previews/000/093/657/non_2x/santa-claus-christmas-background-vector.jpg);
       background-repeat:no-repeat;
       height: 100vh;
      background-size: cover;
      background-position: top;
   
 }


 .bg-video{
     position: absolute;
     top: 0;
     left: 0;
     height: 100%;
     width: 100%;
     z-index: -1;
     opacity: .5;
  overflow: hidden;
 }
 .bg-video__content{
    width: 100%;
    height: 100%;
    object-fit: cover;
 }
.header{
   
    
   color: aliceblue;
  
   display: flex;
   
   justify-content: center;
   align-items: center
  

}

.h1{
    margin-top: 1.9rem;
}
.h1:hover{

    color: rgba(241, 243, 141, 0.582);
}

 .row{
     display: flex;
     max-width:100rem; 
     margin: 4rem  5rem;
     background-color: rgba(255, 255, 255, 0.425);
     justify-content: center;
     flex-direction: column;
    align-items: center;
    padding: 2rem 3rem;
    flex-wrap: wrap;
    font-size: 1rem;
     color:#5e5e5e;
     
    box-shadow: 0 1rem 5rem rgba(0,0,0,.5);
 }

 @media (max-width:600px){
     .row{
         width:100%;
          margin: 2rem  auto;
     }
 }



  .row1{
     display: flex;
     max-width:100rem; 
     margin: 2rem  5rem;
     background-color: rgb(255, 255, 255);
     justify-content: center;
     flex-direction: column;
    align-items: center;
    padding: 2rem 3rem;
    flex-wrap: wrap;
    font-size: 1rem;
     color:#5e5e5e;
      
    box-shadow: 0 1rem 5rem rgba(0,0,0,.5);
 }
  @media (max-width:600px){
     .row1{
         width:100%;
       
          margin: 2rem  auto;
     }
 }
 .inp{
      margin-bottom: 1rem;
      border: none;
      outline: none;
      padding: 1rem 1rem;
      font-size: inherit;
      color: inherit;
      border-bottom: .2rem solid rgb(6, 241, 191);
      box-shadow: 0 1rem 1rem rgba(0,0,0,0.1);
      transition:  all .2s;
 }


    .inp:focus{
        transform: scale(1.1);
        box-shadow: 0 1rem 1rem rgba(0,0,0,0.3);
    }
 @media (max-width:600px){
    .inp:focus{
          transform: none;
        box-shadow:none;
     }
 }
    .inp:focus:invalid{
        border-bottom: .2rem solid rgb(255, 0, 85);
    }
    .inp::-webkit-input-placeholder{
                color:#ccc;        
    }

    .label-primary{
        font-size: 1.3rem;
        margin-top: -3.3rem;
        margin-left: -24rem;
        transition: all .3s;
        color:  rgb(240, 248, 254);
        font-weight: 300;
    }

    .inp:placeholder-shown + .label-primary {
            opacity: 0;
            visibility: hidden;
            transform: translateX(4rem);
        }
@media (max-width:600px){
      .label-primary{
        display: none;
     }
 }


 .btn{
    padding: 1rem 1rem;
    border: none;
    color: inherit;
    outline: none;
    margin-top: 2.5rem; 
    font-size: inherit;
    background-color: rgba(255, 255, 255, 0.979);
    box-shadow: 0 1rem 1rem rgba(0,0,0,0.1);
    border-bottom: .2rem solid rgb(6, 241, 191);
    
    transition:  all .2s;
    cursor: pointer;
   
 }
.btn:disabled,.btn:disabled:hover{
    background-color: rgba(245, 245, 245, 0.568);
    color: rgba(94, 77, 77, 0.658);
    border:none;
     box-shadow:none;
     cursor: not-allowed;
}




 .btn:hover{
  background-color: rgba(0, 255, 255, 0.568);
  color: rgba(0, 0, 0, 0.877);
  box-shadow: 0 1rem 1rem rgba(0,0,0,0.3);
  outline: none
 }
 
 
 .btn:active{
    
      box-shadow: 0 1rem 1rem rgba(0,0,0,0.1);
      background-color: aqua;
 }

.ull{
    display: flex;
    flex-direction: column;
   justify-content: space-between;
    font-size: 1.6rem;
    list-style: none;
    margin-bottom: 2rem;
   
}

 @media (max-width:600px){
     .ull{
        font-size: 1rem;
     }
 }

 .lii:not(:last-child){
     margin-bottom: 1rem;
 }
 .label{
     font-size: 1.2rem;
     color: rgba(255, 0, 0, 0.596);
     word-spacing: .2rem;
     
 }

 .footer{
         display: flex;
    justify-content: flex-end;
    bottom: 0;
    right: 0;
    position: fixed;
      font-family: cursive;
    font-size: .5rem
 }
 .footer__h1{
color: #ccc;

 }
</style>
