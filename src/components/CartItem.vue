<template>
  <li class="cart__item product">
    <div class="product__pic">
      <img
        :src="item.product.image"
        width="120"
        height="120"
        :alt="item.product.title"
      />
    </div>
    <h3 class="product__title">
      {{ item.product.title }}
    </h3>
    <span class="product__code"> {{ item.product.id }} </span>
    <ProductInBasket :count.sync="amount" />
    <b class="product__price">
      {{ (item.amount * item.product.price) | numberFormat }}</b
    >
    <button
      class="product__del button-del"
      type="button"
      aria-label="Удалить товар из корзины"
      @click.prevent="deleteProduct(item.productId)"
    >
      <svg width="20" height="20" fill="currentColor">
        <use xlink:href="#icon-close"></use>
      </svg>
    </button>
  </li>
</template>

<script>
import ProductInBasket from '@/components/ProductInBasket.vue'
import numberFormat from '@/helpers/numberFormat'
import { mapMutations } from 'vuex'

export default {
  data () {
    return {
      counterProduct: 0
    }
  },
  components: { ProductInBasket },
  props: ['item'],
  filters: { numberFormat },
  computed: {
    amount: {
      get () {
        return this.item.amount
      },
      set (value) {
        this.$store.commit('updateCartProduct', {
          productId: this.item.productId,
          amount: value
        })
      }
    }
  },
  methods: {
    ...mapMutations({ deleteProduct: 'deleteCartProduct' })
  }
}
</script>
