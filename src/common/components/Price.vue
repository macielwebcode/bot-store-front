<template>
  <div class="price-box">
    <div class="price-tools">
      <i
        class="fas fa-star"
        v-bind:style="{ color: favorite ? '#269DFF' : '#B5B5C3' }"
        @click="switchFavoriteProduct(id)"
      ></i>
      <div class="form-group">
        <span class="switch switch-sm">
          <label>
            <input type="checkbox" :checked="active" name="select" @click="switchActiveProduct(id)"/>
            <span></span>
          </label>
        </span>
      </div>
    </div>
    <div class="price-img">
      <img :src="require('@/assets/' + image + '.png')" /><br />
      <span>{{ category }}</span>
    </div>
    <br />
    <div class="price-info">
      <span
        ><h4>{{ value }} / Requisição</h4>
        <h4 class="home_txt">{{ name }}</h4></span
      ><br />
      <p>{{ description }}</p>
    </div>
    <div class="verRobos mb-5">
      <a href="#" class="btn btn-white font-weight-bold btn-square mt-20"
        >SAIBA MAIS</a
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    image: {
      type: String,
      required: true
    },
    category: {
      type: Number,
      required: true
    },
    value: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    favorite: {
      type: Boolean,
      required: true
    },
    online: {
      type: Boolean,
      required: true
    },
    active: {
      type: Boolean,
      required: true
    }
  },
  methods: {
     switchActiveProduct(id) {
        this.$emit('switchActiveProduct', id)
     },
     switchFavoriteProduct(id) {
        this.$emit('switchFavoriteProduct', id)
     },
  }
};
</script>

<style></style>
