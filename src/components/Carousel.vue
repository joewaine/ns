<template>
    <main>
      <section :id="offering.category" v-for="offering in offerings" v-bind:key="offering.title" class="section hero is-primary is-fullheight familymeal" :class="offering.category === 'familymeal'">



        <div v-if="offering.visible" class="carousel">
       <h4>{{offering.title}}</h4>
      <carousel :items="offering.slideNo ? offering.slideNo : 3" :loop="true" :dots="false">
          <div v-for="item in offering.items" v-bind:key="item.name" style="text-align:center;">
            <!-- {{item.name}} ${{item.price}} -->
            
            <img v-bind:src="item.img" />
            {{item.description}}
            <div class="order-panel" style="margin-top:10px;">

            <template v-if="item.caviarLink">
              <a :href="item.caviarLink" target="_blank"><Order /></a>
            </template>
              </div>



<div v-if="item.quote">
{{item.quote}}
</div>

          </div>

        </carousel>  


              <div v-if="offering.tockButton" id="mama-dummy-button" class="TockButton-buttonContainer" style="cursor: pointer;">
                <div data-tock-reserve="true" class="TockButton-link">
                  <div class="TockButton TockButton-blue">
                    <span class="TockWidget-B2" @click="loggit()"><OrderStar /></span>
                  </div>
                </div>
              </div>

        </div>

      </section>
    </main>
</template>

<script>

import carousel from 'vue-owl-carousel'


import Order from "@/components/Order";
import OrderStar from "@/components/OrderStar";



export default {
  components: { carousel, Order, OrderStar },
  computed: {
    count () {
      return this.$store.state.count
    },
    names () {
      return this.$store.state.names
    },
    cart () {
      return this.$store.state.cart
    }
  },
  data () {
    return this.$store.state.inventory
  },
  methods: {
    loggit () {
      console.log(134)
    },
    toggle: function (event) {
      if (event.target.classList.contains('is-open')) {
        this.$store.commit('decrement')
        event.target.classList.remove('is-open')
      } else {
        event.target.classList.add('is-open')
        this.$store.commit('increment')
      }
    },
    increment () {
      this.$store.commit('increment')
    },
    decrement () {
      this.$store.commit('decrement')
    },
    increment2 (name) {
      this.$store.commit('increment2', { name })
    },
    removeFromCart (price) {
      this.$store.commit('removeFromCart', { price })
    },
    confirmOrder (timeslot) {
      if (event.target.classList.contains('reserved')) {
        this.$store.commit('unreserveFamilyMeal', { timeslot })
      } else {
        this.$store.commit('reserveFamilyMeal', { timeslot })
      }
    }
  }
}
</script>


<style lang="scss">
.carousel{
  margin-bottom: 100px;
}

.reserved{
  background: red;
}

.not-available{
  background: #666666;
  color: #ffffff;
  pointer-events: none;
}


.order-button{
  width: 33.33%;
  padding: 20px 0;
}


h4{
  text-align: center;
}

.narrow{
  background-color: #F05D5B;


  h4{
        color: #FFF367;
  }
}



[id^=carousel_prev_]{
  position: absolute;
  bottom: -100px;
  left: 0;
}

[id^=carousel_next_]{
  position: absolute;
  bottom: -100px;
  right: 0;
}

</style>