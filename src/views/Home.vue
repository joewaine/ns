<template>
  <div>
<Nav />


      <div class="container mt-5 nav-acc-header">
        <div class="row">
          <div class="col-md-12">
            <ul class="list-group" style="display:none;">
              <li class="list-group-item">Name : {{ user.name }}</li>
              <li class="list-group-item">Email : {{ user.email }}</li>
              </ul>
<ul style="display:none;">
  <li v-for="(item, index) in products">
    {{ item }}
  </li>
  </ul>




<div v-html="body.items[0].elements.body.value">

<!-- {{body.items[0].elements.body.value}} -->

</div>
<SlideShow />


<!-- <Products /> -->
          </div>
        </div>
      </div>

  </div>
</template>
<script>
import VueJwtDecode from "vue-jwt-decode";


import SlideShow from "@/components/SlideShow";

import Products from "@/components/Products";
import Nav from "@/components/Nav";

export default {
    components: {
    SlideShow,
    Products,
    Nav
  },
  data() {
    return {
      user: {},
      products: '',
      body: ''
    };
  },
  methods: {
    // getUserDetails() {
    //   let token = localStorage.getItem("jwt");
    //   let decoded = VueJwtDecode.decode(token);
    //   this.user = decoded;
    // },
    async getUserProducts(){

      // let response = await this.$http.get('/user/' + this.user._id) 
      // // console.log(response.data.user.products)
      // this.products = response.data.user.products
    },
    // logUserOut() {
    //   localStorage.removeItem("jwt");
    //   this.$router.push("/");
    // },
    async showProducts() {




       let response = await this.$http.get('https://deliver.kontent.ai/59d83379-4e1f-00e0-f07e-25ac5dba3666/items').then(result => { 
          // console.log(result.data)
          this.body = result.data
        })







    }
    
  },
  created() {
    // this.getUserDetails();
    // this.getUserProducts();
    this.showProducts();

  }

};
</script>

<style scoped>


.fix-top-nav{
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 100;
}


.section.hero{
  width: 100%;
  height: 100vh;
}




.nav-acc-header{
  padding-top: 140px;
}


@media only screen and (max-width: 1080px) {

.nav-acc-header{
  padding-top: 80px;
}

}

</style>