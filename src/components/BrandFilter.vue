<template>
  <div class="filter">
    <select @change="handleChange">
      <option value="">All Brands</option>
      <option v-for="brand in brands" :value="brand" :key="brand">
        {{ brand }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    brands: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedBrand: '',
    };
  },
  methods: {
    handleChange(event) {
      this.selectedBrand = event.target.value;
      this.$emit('brandSelected', this.selectedBrand);
    },
  },
};
</script>
