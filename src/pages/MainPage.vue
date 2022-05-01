<template>
  <main class="content container">
    <div class="content__top content__top--catalog">
      <h1 class="content__title">Каталог</h1>
      <span class="content__info"> 152 товара </span>
    </div>
    <div class="content__catalog">
      <ProductFilter
        :price-from.sync="filterPriceFrom"
        :price-to.sync="filterPriceTo"
        :category-id.sync="filterCategoryId"
        :color-id.sync="filterColor"
      />
      <section class="catalog">
        <ProductList :products="products" />
        <BasePagination
          v-model="page"
          :count="countProducts"
          :per-page="productsPerPage"
        />
      </section>
    </div>
  </main>
</template>
<script>
import products from '@/data/products'
import ProductList from '@/components/ProductList.vue'
import BasePagination from '@/components/BasePagination.vue'
import ProductFilter from '@/components/ProductFilter.vue'

export default {
  components: { ProductList, BasePagination, ProductFilter },
  data () {
    return {
      filterColor: '#73b6ea',
      filterPriceFrom: 0,
      filterPriceTo: 0,
      filterCategoryId: 0,
      page: 1,
      productsPerPage: 3
    }
  },
  computed: {
    filteredProducts () {
      let filteredProducts = products

      if (this.filterColor > 0) {
        filteredProducts = filteredProducts.filter(product => {
          const item = product.colors.filter(color => {
            console.log(color.id === this.filterColor)
            return color.id === this.filterColor
          })
          return item.length > 0
        })
      }

      if (this.filterPriceFrom > 0) {
        filteredProducts = filteredProducts.filter(
          (product) => product.price > this.filterPriceFrom
        )
      }

      if (this.filterPriceTo > 0) {
        filteredProducts = filteredProducts.filter(
          (product) => product.price <= this.filterPriceTo
        )
      }
      if (this.filterCategoryId > 0) {
        filteredProducts = filteredProducts.filter(
          (product) => product.categoryId === this.filterCategoryId
        )
      }
      return filteredProducts
    },
    products () {
      const offset = (this.page - 1) * this.productsPerPage

      return this.filteredProducts.slice(offset, offset + this.productsPerPage)
    },
    countProducts () {
      return this.filteredProducts.length
    }
  }
}
</script>
