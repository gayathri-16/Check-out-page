 
 <template>
  <div id="app">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@200;300&family=Nunito+Sans:ital,wght@0,600;1,200;1,300&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.10.1/css/all.css">
    <link rel="stylesheet" href="https://michalsnik.github.io/aos/">  
    <link rel="stylesheet" href="https://unpkg.com/aos@2.3.1/dist/aos.css"> 
      
      <h1> CheckOut</h1>
   <div class="form">
      <h2>Contact information</h2>
        <form @submit="processForm" id="signup-form">
          <label for="Enter your E-mail">E-mail</label><br>
          <input type="text" class="mail" v-model="email"  name="email" placeholder="  Enter your email..."> <i class="fas fa-envelope " style="color:gray;"></i>
          <br> <p v-if="errors.email">Please enter a valid email</p>
          <label for="">Phone</label><br>
          <input type="text" class="ph-no" v-model="phone" name="phone"  placeholder="Enter your phone no..."><i class="fas fa-phone-alt" style="color:gray;"></i>
     <h3>Shipping address</h3>
          <label for="">Full name</label><br>
          <input type="text" v-model="fullname" name="fullname" > <i class="fas fa-user-circle" style="color:gray;"></i> <br>
          <label for="">Address</label> <br>
          <input type="text"  v-model="address" name="address" placeholder="Your address..."><i class="fas fa-home" style="color:gray;"></i><br>
          <label for="">City</label> <br>
          <input type="text" v-model="city" name="city" placeholder="Your city..."> <i class="fas fa-city" style="color:gray; font-size:14px;"></i> <br>
          <label for="" >Country <span id="code">Postal code</span></label> <br>
            
            <select v-model="country"  class="select" > <br> <i class="fas fa-home" style=" position:absolute; color:gray;"></i> 
                <option value=""> Select option</option>
                <option value=""> India</option>
                <option value=""> USA</option>
                <option value=""> United Kingdom</option>
                <option value=""> Australiya</option>
                <option value=""> England</option>
                <option value=""> Rusia</option>
           </select>
   <input type="text" v-model="postalcode" id="post"  placeholder="Your postal code.." > <i class="fas fa-mail-bulk" id="post-icon"></i> <br>
   <input type="checkbox" style="margin-top:1rem;"> <label for="">Save this information for next time</label> <br>
   <button type="button" @click="processForm" class="btn" >Continue</button>
 </form> 
  
<div class="goods">
  <nav class="nav">
  <div class="cart">
    <button @click="showCart =!showCart" class="cart-btn" style="position:fixed;">
      <i class="fas fa-shopping-cart" style="margin-left:0.1rem; "></i>
      <span class="total-items"><sup> {{totalQuantity}} </sup></span>
    </button>
    
  <div v-if="showCart" class="cart-dropdown">
      <ul class="dropdown_list">
        <li v-for="product in cart" :key="product.id"> {{product.name}} ({{product.quantity}}) </li>
      </ul>
  </div>
</div>
</nav>

  <section>
  <div v-for="product in products" :key="product.id" class="items">
   
    <h6>{{ product.name }}</h6>
     <p> ${{product.rate}} <span>${{product.save}}</span></p>
      <img v-bind:src="product.src" alt=""> 
   
    <div class="no-of-items">
      <button @click="updateCart(product, 'subtract')" class="decrease">-</button>
      <span id="number" style="text-decoration:none;"> {{product.quantity}}
      <button @click="updateCart(product, 'add')" class="increase">+</button></span>
    </div>
 
  </div>
 
      <div class="shipping">
        <hr> <h1 class="ship" >Shipping <span style=" font-size:18px; color:black; margin-left:13rem;">$19</span> </h1><hr>
              <h1  class="total" >Total <span id="amount" style=" font-size:18px; color:black; margin-left:13.5rem;">  $ {{totalAmount}} </span>  </h1>
      </div>
  
  </section> 
</div>

       </div>
  </div>
</template>
<script>

  export default {
    el:'#signup-form',
    data(){
      
      return{
       email:'',
       phone:'',
       fullname:'',
       address:'',
       city:'',
       country:'',
       postalcode:'',
       errors:{
         email:false,
         phone:false
       },
        products:[
            {
            id:1,
            name: 'Bag',
            quantity:0,
            src:'https://www.bhphotovideo.com/images/images2500x2500/CineBags_cb_23a_CB23_DSLR_HD_874536.jpg',
            rate:54.99,
            save:'94.99'
             
          },
          {
            id:2,
            name: 'Shoes',
            quantity:0,
            src:'http://getwallpapers.com/wallpaper/full/0/4/8/931607-beautiful-basketball-shoes-wallpapers-1920x1080-samsung-galaxy.jpg',
            rate:74.99,
            save:'124.99'
          }
          ],
          showCart:false
      };
    },
    
    computed:{
      cart(){
        return this.products.filter(product => product.quantity >0);
      },
      totalQuantity(){
        return this.products.reduce(
          (total, product)=> total + product.quantity,
          0
        );
        },
        totalAmount(){
        return this.products.reduce(
          (total, product)=> {
            return total + product.rate * product.quantity
          },0 )
        }

      },
      methods: {
       
      processForm:function(){
        
        if(this.email=='' || this.phone==''){
           alert("Validation Fails");
        }
     
        else{
          alert("success")
        }
      },
     
        updateCart(product, updateType){
          for (let i=0; i<this.products.length; i++){
            if(this.products[i].id===product.id){
              if(updateType==='subtract'){
                if(this.products[i].quantity !== 0){
                  this.products[i].quantity--;
                }
              }    else{
                     this.products[i].quantity++;

              }
              break;
            }
          }
        }
      },

    }
  
</script>

<style>
#app{
 margin-top:-1.5rem;
 margin-left:-1.5rem;
  margin-right:1.5rem;
 background-image:url(/.assets/bg.jpg) no-repeat;
 background-size:cover ;
 
 width:105%; 

 height:750px;
  background:black;
}

.cart-btn{
  background: transparent;
  border: none;
  float:right;
}
.cart-btn:focus{
  outline:none;
}
.cart{
 margin-left:24.5rem;
 position:relative;
 
}
#post-icon{
  margin-left:-10.5rem;color:gray;
}
.dropdown_list{
   list-style: none;
   position:absolute;
   
  }
 .total-items{
 
  color:black;
 
}
.cart-dropdown{
   width:100px;
   height:60px;
  
   border-radius:10px;
  
   
}
li{
  color:black;
  margin-left:-2rem;
 text-align:left;
 
 
}
#code{
   margin-left:15rem;
}
h1{
  padding-top:3rem;
  margin-left:15rem;
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  color:white;
}
h2{
  font-size:24px;
  color:rgb(172, 169, 169);

}
h3{
  color:rgb(172,169,169);
}
.form{
  width:100%;
  height:auto;
  margin-left:15rem;
  margin-top:2rem;
  align-items:center;
  background: black;

  
}
.form input[type="text"]
  
  {
   padding-left:37px;
   font-size:16px;
   font-family:'Poppins' sans-serif;
   width:500px;
   text-align: left;
   height:40px;
   border-radius:10px;
   border: 2px solid #3498db;
   margin-top:0.5rem;
   margin-bottom: 0.1rem;
   background:black;
   outline:none;
   color:white;
  
  }
  .form input[type="text"]:focus{
    border-color:#2ecc71;
  }
  .form i{
    margin-left:-33.3rem;
    left:0;
    top:8px;
    padding:0.1rem;
    font-size:20px;

  }
  .ph-no
  {
   width:500px;
   height:45px;
   border-radius:10px;
   border: 0.2px solid gray;
   margin-top:0.3rem;
   margin-bottom: 0.3rem;
  }
  label{
    color:rgb(233, 224, 224);
  }
  .btn{
    margin-left:18rem;
   
    width:180px;
    height:40px;
    border-radius:10px;
    color: #fff;
    font-size:18px;
    background: transparent;
    border:2px solid rgb(241, 86, 14);
  }
  .btn:hover{
     background:rgb(241, 86, 14);
  }
   .btn:focus{
     outline:none;
   }
  .goods{
    width:480px;
    height:550px;
    background: rgb(233, 230, 230);
    float:right;
    margin-top:-40rem;
    margin-right:22rem;
    border-radius: 15px;

    
  }
  .items img{
    width:150px;
    height:150px;
    border-radius:15px;
    margin-left:-15rem;
    margin-top:-5rem;
  }
 .items{
  
   color:gray;
   margin-left:18rem;
   margin-right:4rem;
   margin-top:-2.5rem;
 }
 .items h6{
   font-size:20px;
   font-family:'Poppins', sans-serif;
   margin-left:-3rem;
   color:rgb(53, 51, 51);
 }
.items p{
  font-size:20px;
  color:rgb(248, 105, 53);
  margin-top:-2rem;
  margin-left:-3rem;
  font-weight:bold;
}
.items span{
  color:rgb(59, 59, 59);
  text-decoration: line-through;
  font-size:16px;
  margin-left:1rem;
}
.items .no-of-items
{
  width:150px;
  height:60px;
  background:rgb(253, 249, 249);
  margin-top:-5rem;
  margin-left:-3rem;
  border:1px solid gray ;
  border-radius:15px;
  position:absolute;
} .decrease {
  margin-left:1rem;
  margin-top:1rem;
  font-size:24px;
  color:rgb(94, 93, 93);
  border-radius:5px;
  background:rgb(211, 204, 204);
  width:35px;
  height:35px;
  border-style:none;
  
}
.increase{
   margin-left:1rem;
  margin-top:1rem;
  font-size:24px;
  color:rgb(78, 78, 78);
  width:35px;
  height:35px;
  background:rgb(211, 204, 204);
  border-style:none;
  border-radius:5px;
}
 hr{
   width:380px;
   
 }
.ship{
  color:black; font-size:24px; padding:0; margin-left:3.4rem;}

  .total{
  color:black; font-size:24px; padding:0; margin-left:3.4rem;}
  
 .shipping{
   margin-top:2rem;

}
#number{
   text-decoration:none;
   color:black;
   font-size:24px;
    font-family:'Poppins';
    display:inline;
    
}
.select{
  width:230px;
   height:45px;
   border-radius:10px; 
  margin-right:-5rem;
  background: transparent;
  border: 2px solid #3498db;
  color:gray;
  padding:10px 25px;
  font-size:15px;
}
select:focus{
  outline:none;
}
#post{
  width:210px; 
   margin-right:-5rem; 
   margin-left:8.5rem; 
  margin-top:-5.5rem;
}

@media only screen and (max-width:600px){
  #app{
    width:110%;
    height:auto;
  }
  .form{
  width:100%;
  height:auto;
  margin-left:4rem;
  margin-top:23rem;
  align-items:left;
  
}
.form i{
    margin-left:-19rem;
   
    font-size:20px;

  }
  ::-webkit-input-placeholder{
    font-size:15px;
    padding:2rem;
   
  }
h1{
  margin-top:-2rem;
  margin-bottom:1.5rem;
  margin-left:2.5rem;
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  color:white;
}
h2{
  margin-top:-1rem;
  font-size:20px;
  color:rgb(172, 169, 169);

}
h3{
  font-size:18px;
  margin-top:0.5rem;
  color:rgb(172,169,169);
}
#post-icon{
  margin-left:-4.5rem;color:gray;
  font-size:15px;
}
.select{
  width:130px;
   height:35px;
   border-radius:10px; 
  margin-right:-5rem;
  background: transparent;
  border: 2px solid #3498db;
  color:gray;
  padding:1px 2px;
  font-size:15px;
}
#post{
  width:150px; 
  height:28px;
   margin-right:-5rem; 
   margin-left:6rem; 
  margin-top:-5rem;
}
#code{
  margin-left:6rem;
}

.form input[type=text]
  
  {
   padding-left:5px;
   font-size:16px;
   font-family:'Poppins' sans-serif;
   width:300px;
   height:35px;
   border-radius:10px;
   
   margin-top:0.1rem;
   margin-bottom: 0.1rem;
  }
   .btn{
    margin-left:15rem;
   
    width:100px;
    height:40px;
    border-radius:10px;
    color: #fff;
    font-size:15px;
    background: transparent;
    border:2px solid rgb(241, 86, 14);
  }
  .goods{
    width:400px;
    height:300px;
    background: rgb(233, 230, 230);
    margin-top:-53rem;
    margin-left:-2rem;
    border-radius: 15px;
    float:left;

    
  }
  .items img{
    width:85px;
    height:85px;
    border-radius:15px;
    margin-left:-7rem;
    margin-top:-4rem;
  }
 .items{
  
   color:gray;
   margin-left:8rem;
   margin-right:3rem;
   
 }
 .items h6{
   font-size:18px;
   font-family:'Poppins', sans-serif;
   margin-left:1rem;
   margin-top:3.2rem;
   color:rgb(53, 51, 51);
 }
.items p{
  font-size:18px;
  color:rgb(248, 105, 53);
  margin-top:-2.2rem;
  margin-left:1rem;
  font-weight:bold;
}
.items span{
  color:rgb(59, 59, 59);
  text-decoration: line-through;
  font-size:16px;
  margin-left:1rem;
}
.items .no-of-items
{
  width:100px;
  height:20px;
  background:rgb(253, 249, 249);
  margin-top:-2rem;
  margin-left:1rem;
  padding:8px 5px;
  border:1px solid gray ;
  border-radius:15px;
  position:absolute;
} .decrease {
  margin-left:0.5rem;
  margin-top:-0.1rem;
  font-size:14px;
  color:rgb(94, 93, 93);
  border-radius:5px;
  background:rgb(211, 204, 204);
  width:25px;
  height:25px;
  border-style:none;
  position:absolute;
  
}
.increase{
  position:absolute;
  margin-top:-0.1rem;
  margin-left:0.8rem;
  font-size:15px;
  color:rgb(78, 78, 78);
  width:25px;
  height:25px;
  background:rgb(211, 204, 204);
  border-style:none;
  border-radius:5px;
}
 hr{
   width:380px;
   margin-top:-0.5rem;
   
 }
 .ship {
   font-size:14px;
   margin-top:-0.8rem;
   margin-left:2rem;
  
 }
 .total {
   font-size:14px;
   margin-top:-0.3rem;
   margin-left:2rem;
 }
 #number{
   text-decoration:none;
   color:black;
   font-size:20px;
    font-family:'Poppins';
    
   margin-left:3rem;
   text-align:center;
   padding-bottom:1px ;
}
.cart{
 margin-left:21rem;
 margin-top:0.5rem;
 position:relative;
 
}
.cart:focus{
  border-style:none;
}
.dropdown_list{
   list-style: none;
   position:absolute;
   font-size:12px;
  
   
  }
 .total-items{
 
  color:black;
 
}
.cart-dropdown{
   width:100px;
   height:60px;
   position:fixed;
   border-radius:10px;
   margin-left:-0.8rem;
    margin-top:1.5rem;
  
   
}
li{
  color:black;
  margin-left:-2rem;
 text-align:left;
 
 
}
#amount{
  font-size:12px;
}
 }
  </style>
