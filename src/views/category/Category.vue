<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h3 class="pt-3">Our Categories</h3>
        <router-link :to="{name: 'AddCategory'}">
          <button class="btn" style="float:right">Add Category</button>
        </router-link>
      </div>
    </div>
    <div class="row">
      <div v-for="category in categories" :key="category.id" class="col-xl-4 col-md-6 col-12 pt-3 d-flex">
        <CategoryBox :category="category"></CategoryBox>
      </div>
    </div>
  </div>
</template>

<script>
import CategoryBox from "@/components/category/CategoryBox";
const axios = require("axios")
export default {
  name: "AddCategory",
  components: {CategoryBox},
  data() {
    return {
      baseUrl: "http://localhost:8081",
      categories: []
    }
  },
  methods: {
    async getCategories() {
      await axios.get(`${this.baseUrl}/category/list`)
      .then(resp => this.categories = resp.data)
      .catch(err => console.log(err))
    }
  },
  mounted() {
    this.getCategories()
  }
}
</script>

<style scoped>

</style>