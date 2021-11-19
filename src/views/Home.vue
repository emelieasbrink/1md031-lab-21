<template>
  <header>
    <img src="https://freedesignfile.com/upload/2016/10/Beautiful-sky-Stock-Photo-01.jpg"
    alt="A sky with clouds" title="Cloudy sky">
    <h1>Welcome to BurgerHeaven Online</h1>
  </header>

    <main>
      <section id="selectburger">

  <h2>Select burgers</h2>

  <p>This is where you select burger/burgers you are in the mood for today.</p>

  <div class=wrapper>
      <Burger v-for="burger in burgers"
          v-bind:burger="burger"
          v-bind:key="burger.name"
          v-on:orderedBurger="addToOrder($event)"/>
    </div>

    </section>

      <section id="customerinfo">
  <h2 style="clear:left;"> Customer information </h2>
  <p>This is where you provide neccessary information about yourself.</p>

  <form>
    <p>
      <label for="fullname">Full name</label><br>
      <input type="text" id="fullname" v-model="name" required="required" placeholder="First- and lastname">
    </p>

    <p>
      <label for="email">Email address</label><br>
      <input type="email" id="email" v-model="email" placeholder="E-mail address">
    </p>

  <p>
    <label for="payment">Payment options</label><br>
      <select id="payment" v-model="payment">
        <option>Credit card</option>
        <option>Swish</option>
        <option>Paypal</option>
        <option>Invoice</option>
      </select>
    </p>

    <p>
      <label for="female">Gender</label><br>
      <input type="radio" id="female" v-model="gender" value="female">
      <label for="female">Female</label><br>

      <input type="radio" id="male" v-model="gender" value="male">
      <label for="male">Male</label><br>

      <input type="radio" id="nonbinary" v-model="gender" value="nonbinary">
      <label for="nonbinary">Non-binary</label><br>

      <input type="radio" id="undisclosed" v-model="gender" value="undisclosed">
      <label for="undisclosed">Do not wish to provide</label><br>
    </p>

    </form>

    <p> Select point of delivery:
    </p>

    <div class=scroll>
      <div id="map" v-on:click="setLocation">
        <div v-bind:style="{ left: this.location.x + 'px', top: this.location.y + 'px' }">
            T
          </div>
      </div>
    </div>


    </section>

    <button type="submit" v-on:click="addOrder">
      <img src="https://thumbs.dreamstime.com/b/fast-burger-logo-running-background-white-eps-196319997.jpg"
      style="width: 35px;">
      Place my order
    </button>

    </main>

      <footer>
        </footer>

</template>

<script>
import Burger from '../components/Burger.vue'
import menu from '../assets/menu.json'
import io from 'socket.io-client'

const socket = io();

    /*  Menu Constructor (never used):
function MenuItem(na, pic, kcal, lac, gl) {
    this.name = na;
    this.url = pic;
    this.kCal = kcal;
    this.lactose = lac;
    this.gluten = gl;
    }

   const myBurgers=[new MenuItem("The Cheesy Burger", "https://twisper.com/wp-content/uploads/2020/03/close-up-photo-of-burger-3915906-scaled.jpg",
   2000,true, false),
   new MenuItem("The Chicken Dream", "https://www.ilovecooking.ie/wp-content/uploads/2021/05/Korean-Style-Chicken-Burger-Final-Online-HR-3161-scaled-6.jpg",
   700,true, false),
   new MenuItem("The NoMeat Burger", "https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/vegan-burger-2-1578931709.jpg",
   500,false, true)];

      */


export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu,
      name: '',
      email: '',
      gender: 'undisclosed',
      payment: 'Credit card',
      orderedBurgers: {"The Cheesy Burger": 0,
                       "The Chicken Dream": 0,
                       "The NoMeat Burger": 0
                      },
      location:{x:0,
                y:0
              }
    }
  },

  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },

    setLocation: function(event){
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location.x = event.clientX - 10 - offset.x;
      this.location.y = event.clientY - 10 - offset.y;
    },

    addOrder: function() {
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: this.location.x,
                                           y: this.location.y
                                         },
                                customerInfo: {fn: this.name,
                                              em: this.email,
                                              gend: this.gender,
                                              pay: this.payment
                                            },

                                orderItems: this.orderedBurgers
                              }
                 );
      console.log(this.name, this.email, this.payment, this.gender, this.orderedBurgers);
    },

    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
    }
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Average';
body {
   font-family: Average, sans-serif;
   font-size: 14pt;
}


#selectburger{
  border: 2px dotted black;
  padding-right: 2em;
  padding-bottom:2em;
  background-color: white;
  color: black;
}

#customerinfo {
  background-color: black;
  color: white;
  border: 2px dotted white;
  padding-bottom: 1em;
}

button:hover {
   background-color: LightGreen;
   cursor: pointer;
}

section {
  margin: 2em;
  padding-left: 2em;
  }

button{
  margin-left: 1em;
  margin-bottom: 1em;
  }

  .wrapper {
       display: grid;
       grid-gap: 10px;
       grid-template-columns: 350px 350px 350px;
       border-style: double;
       padding-left: 6em;
   }

   header {
     margin: 2em;
     overflow:hidden;
     height: 12em;
   }

   header img {
     opacity: 0.4;
     width: 100%;
     height: auto;
   }

   header h1 {
     position: absolute;
     padding: 1.5em;
     padding-left:10em;
     margin-top: -60%;
   }

  #map {
    position: absolute;
    background: url("/img/polacks.jpg");
    background-repeat: no-repeat;
    width:1920px;
    height: 1078px;
  }

  .scroll{
    position: relative;
    width:1100px;
    height: 500px;
    overflow: scroll;
  }

  #map div {
    position: absolute;
    background: black;
    color: white;
    border-radius: 10px;
    width:20px;
    height:20px;
    text-align: center;
  }

</style>
