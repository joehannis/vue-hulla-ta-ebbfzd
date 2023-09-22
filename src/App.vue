<template>
  <div class="app" ref="app-container">
    <div class="header">
      <p class="filters">
        <BrandFilter :brands="brands" @brand-selected="handleBrandSelected" />
        <StockFilter
          :stock-statuses="stockStatuses"
          @selected-stock-status="handleStockStatusSelected"
        />
        Total: {{ counter }}
      </p>
    </div>
    <div class="app">
      <div class="no-products" v-if="filteredProductList.length === 0">
        There are no products
      </div>
      <div class="card">
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

<style >
  .filters {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: flex-end;
    margin: 10px;
    width: 80%;
    height: 50px;
    background-color: #f2e0c1;
    border-radius: 4px;
    margin-bottom: 20px;
  }
  .list {
  list-style-type: none;
  padding: 0;
  justify-content: center;
  }
  .app {
    display: flex;
    flex-direction: column;

  }
}

</style>

<script>
import ProductGridItem from './components/ProductGridItem.vue';
import products from './data/products.json';
import BrandFilter from './components/BrandFilter.vue';
import StockFilter from './components/StockFilter.vue';

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
      counter: products.length
    };
  },
  methods: {
    filterProducts() {
      this.filteresProductList = []
      this.filteredProductList = this.products.filter((product) => {
        if (this.selectedBrand && product.brand !== this.selectedBrand) {
          return false; 
        }

        if (this.selectedStatus !== '') {
          return product.isAvailable === this.selectedStatus; 
        }

        return true;
      });
      if (this.filteredProductList.length > 0) {
        this.counter = this.filteredProductList.length;
      } else {
        this.counter = this.products.length;
      }
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



