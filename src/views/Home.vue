<template>
  <div class="info-box">
    <!--end::Aside-->

    <!--begin::Row-->
    <div class="row">
      <div class="col-xl-12">
        <div class="d-flext row">
          <div class="col-md-3 col-12 mt-5">
            <Card
              @filterCategory="filterCategory($event)"
              @filterProductsActive="filterProductsActive()"
              @filterFavorite="filterFavorite()"
              :categories="categories"
              :favoriteActive="favoriteActive"
            />
          </div>
          <div class="col-md-9 col-12 mt-5">
            <Search 
            @keyPress="keyPress()"/>
            <div class="price-area" v-if="!emptyPriceData">
              <Price
                v-for="product in productsSearch"
                :key="product.id"
                :id="product.id"
                :image="product.image"
                :name="product.name"
                :description="product.description"
                :value="product.value"
                :favorite="product.favorite"
                :active="product.active"
                :online="product.online"
                :category="product.category"
                @switchActiveProduct="switchActiveProduct($event)"
                @switchFavoriteProduct="switchFavoriteProduct($event)"
              />
            </div>
            <div class="col-md-12 col-12" v-else>
              <div
                class="Search_Empty"
                :style="avatarBackgroundImage"
              >
                <!-- <img src="assets/media/site-images/empty.png"> -->
                <div class="Search_Empty_txt">
                  <h2>Ops! nenhum resultado encontrado.</h2>
                  <span>O que eu faço?</span>
                  <p>
                    Verifique os termos digitados ou os filtros
                    selecionados.Utilize termos genéricos na busca.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Card from "@/common/components/layout/Card";
import Search from "@/common/components/Search";
import Price from "@/common/components/Price";
export default {
  name: "Default",
  data() {
    return {
      lastCategory: false,
      favoriteActive: false,
      activeProductsActive: false,
      categories: [],
      products: [],
      productsSearch: [],
      avatarBackgroundImage: {
          backgroundImage: `url(${require('@/assets/media/site-images/empty.png')})`
        }
    };
  },
  components: {
    Card,
    Search,
    Price,
  },
  computed: {
    emptyPriceData() {
      return this.productsSearch.length === 0;
    },
    
  },
  methods: {
    filterCategory(event) {
      if(this.lastCategory == event){
        this.productsSearch = this.products;
        this.lastCategory = false;
      } else{
        this.lastCategory = event;
        this.productsSearch = this.products.filter((p) => p.category === event);
      }
      this.favoriteActive = false;

      this.categories.forEach(c => {
        c.id === event ? c.active = this.lastCategory == event : c.active = false;
      })
    },
    filterFavorite() {
      if(this.favoriteActive){
        this.productsSearch = this.products;
        this.favoriteActive = false;
      } else {
        this.productsSearch = this.products.filter((p) => p.favorite === true);
        this.favoriteActive = true;
      }
      this.categories.forEach(c => c.active = false);
    },
    filterProductsActive() {
      if(this.activeProductsActive){
        this.productsSearch = this.products;
        this.activeProductsActive = false;
      } else {
        this.productsSearch = this.products.filter((p) => p.active === true);
        this.activeProductsActive = true;
      }
    },
    async getCategories() {
      try{
        const endpoint = "/categories";
        const response = await axios.get(endpoint)

        const results = response.data
        this.categories = results.filter(category => category.layout_active == 1).map(category => ({
          id: category.id,
          name: category.title,
          active: false,
        }))
      } catch(err){
        if(err.response)
          console.log("Server error: " + err);
        else if(err.request)
          console.log("Network error: "+ err);
        else
          console.log("Client error: "+ err);
      }
    },
    async getProducts() {
      try{
        const endpoint = "/products";
        // const body = {
        //   category: category
        // };
        const response = await axios.get(endpoint)//, body)
        const results = response.data
        this.products = results.filter(product => product.layout_active == 1).map(product => ({
          id: product.id,
          image: "media/site-images/back-office",
          name: product.name,
          description: product.description,
          value: product.value,
          category: product.category_id,
          active: true,
          favorite: false,
          online: true
        }))
        this.productsSearch = this.products
      } catch(err){
        if(err.response)
          console.log("Server error: " + err);
        else if(err.request)
          console.log("Network error: "+ err);
        else
          console.log("Client error: "+ err);
      }
    },
    async switchActiveProduct(product) {
      const endpoint = "/products/switchactivation/" + product;

      // TODO: call post action to switch product

      this.products = this.products.map(p => {
        if(p.id == product)
          p.active = !p.active;
        return p;
      })

    },
    async switchFavoriteProduct(product) {
      const endpoint = "/products/switchfavorite/" + product;

      // TODO: call post action to switch favorite product

      this.products = this.products.map(p => {
        if(p.id == product)
          p.favorite = !p.favorite;
        return p;
      })

    }

  },
  watch: {
    $route(to, from) {
      to.query.favorite ? this.filterFavorite() : to.query.sectors ? this.filterCategory(to.query.sectors) : null;
    },
  },
  created() {
    this.getCategories()
    this.getProducts()
  },
  mounted() {
    const route = this.$route;
    route.query.favorite ? this.filterFavorite() : route.query.sectors ? this.filterCategory(route.query.sectors) : null;
  }
};
</script>

<style></style>
