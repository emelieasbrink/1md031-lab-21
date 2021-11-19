<template>

  <div>
    <h3>{{ burger.name }}</h3>
    <img v-bind:src="burger.url">

    <ul>
      <li>{{ burger.kCal + " kCal"}}  </li>
       <span v-if=burger.lactose>
        <li> Contains <span class="ingredient"> lactose </span>
          </li>
        </span>

       <span v-if=burger.gluten>
        <li> Contains <span class="ingredient"> gluten </span>
        </li>
        </span>
    </ul>

    <p> Amount:
    <button v-on:click="removeBurger">
    - </button>

    {{amountOrdered}}

    <button v-on:click="addBurger">
    + </button>
    </p>
    </div>

</template>

<script>

export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function () {
  return {
    amountOrdered: 0,
  }
  },

  methods: {
  addBurger: function(){
    this.amountOrdered+=1;
    this.$emit('orderedBurger', { name:   this.burger.name,
                                amount: this.amountOrdered
                              }
    );
  },
  removeBurger: function(){
    this.amountOrdered-=1;
    this.$emit('orderedBurger', { name:   this.burger.name,
                                amount: this.amountOrdered
                              }
  );
  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 .ingredient {
    font-weight: bold;
 }

 button{
   margin-right: 1em;
   }

   button:hover {
      background-color: LightBlue;
      cursor: pointer;
   }

   img {
          width: 200px;
     }


</style>
