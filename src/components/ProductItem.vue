<template>
  <li class="catalog__item">
    <router-link
      class="catalog__pic"
      :to="{name:'product',params:{id:product.id}}"
    >
      <img :src="product.image" :srcset="product.src" alt="product.title" />
    </router-link>

    <h3 class="catalog__title">
      <a href="#"> {{ product.title }} </a>
    </h3>

    <span class="catalog__price"> {{ product.price | numberFormat }} </span>

    <ul class="colors colors--black">
      <li
      class="colors__item"
      v-for="productColor of product.colors"
      :key="productColor.id"
      >
        <label class="colors__label" >
          <input
            class="colors__radio sr-only"
            type="radio"
            :value="productColor.id"
            v-model="ProductColor"
          />
          <span class="colors__value" :style="{backgroundColor: productColor.code}"> </span>
        </label>
      </li>
    </ul>
  </li>
</template>

<script>
import numberFormat from '@/helpers/numberFormat'

export default {
  data () {
    return {
      ProductColor: '#73B6EA'
    }
  },
  filters: {
    numberFormat
  },
  props: ['product']
}
</script>
