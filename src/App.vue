<template>
  <div class="app" ref="app-container">
    <div class="header">
      <p class="filters">
        <BrandFilter :brands="brands" @brand-selected="handleBrandSelected" />
        <StockFilter
          :stock-statuses="stockStatuses"
          @selected-stock-status="handleStockStatusSelected"
        />
        <p>Total: {{ counter }}</p>
      </p>
    </div>
    <div class="app">
      <div class="no-products" v-if="filteredProductList.length === 0">
        There are no products
      </div>
      <div class="product-grid">
        <ul class="list">
          <li
            class="card"
            v-for="product in filteredProductList"
            :key="product.brand"
          >
            <ProductGridItem :product="product" />
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import ProductGridItem from './components/ProductGridItem.vue';
import products from './data/products.json';
import BrandFilter from './components/BrandFilter.vue';
import StockFilter from './components/StockFilter.vue';
console.log(products[1].isAvailable);

export default {
  name: 'App',
  components: {
    ProductGridItem,
    BrandFilter,
    StockFilter,
  },
  data() {
    return {
      products,
      brands: [...new Set(products.map((product) => product.brand))],
      stockStatuses: [
        ...new Set(products.map((product) => product.isAvailable)),
      ],
      filteredProductList: products,
      selectedBrand: '',
      selectedStatus: '',
      counter: filteredProductList.length
    };
  },
  methods: {
    filterProducts() {
      this.filteredProductList = this.products.filter((product) => {
        if (this.selectedBrand && product.brand !== this.selectedBrand) {
          return false; // Filter out products with a different brand
        }

        if (this.selectedStatus !== '') {
          console.log(product.isAvailable);
          console.log(this.selectedStatus);
          return product.isAvailable === this.selectedStatus; // Filter based on selectedStatus
        }

        return true; // No brand or status filter applied
      });
    },

    handleBrandSelected(brand) {
      this.selectedBrand = brand;
      this.filterProducts();
    },
    handleStockStatusSelected(status) {
      this.selectedStatus = status;
      this.filterProducts();
    },
  },
};


