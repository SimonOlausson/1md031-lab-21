<!--
  Keep data seperate from the template, the template will work for severeal different burgers
  Data could be kept in a menu.json file.
-->
<template>
  <div>
    <div>
      <button type="button" v-on:click="minusAmount">
        minus
      </button>
      <button type="button" v-on:click="plusAmount">
        plus
      </button>
    </div>
    <h2> {{ burger.name }} {{amountOrdered}} </h2>
    <img id="burgarbild" v-bind:src="burger.image">
    <section class="ingredienser">
      <ul>
        <li>Innehåller kött</li>
        <li v-if="burger.gluten">Innehåller gluten</li>
        <li v-else> Glutenfri</li>
        <li v-if="burger.lactose">Innehåller laktos</li>
        <li v-else> laktosfri</li>

      </ul>
    </section>
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
    plusAmount: function () {
       this.amountOrdered = this.amountOrdered + 1
      this.$emit('orderedBurger', {
                                    name:this.burger.name,
                                    amount:this.amountOrdered}

      )
    },
    minusAmount: function () {
      this.amountOrdered = this.amountOrdered -1
      this.$emit('orderedBurger', {
                                    name:this.burger.name,
                                    amount:this.amountOrdered}

      )
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.ingredienser {
  color: #ff5500;
  font-weight: bold;
}
#burgarbild{
  width: auto;
  height: 200px;
}


</style>
