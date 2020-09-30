<template>
    <!-- Modal -->
 <button type="button" class="btn btn-primary " data-toggle="modal" data-target="#exampleModal">
        Filters
 </button>
 
 <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
   <div class="modal-dialog" role="document">
     <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">News filter</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
    </div>
    <div class="modal-body">
            <h6 class="filter-label">Select Country Feed</h6>
            <select class="form-control mb-4" v-model="country"  >
            <option value="" selected disabled hidden>Country</option>
            <option  v-for="country in countries" v-bind:key="country.id" :value="country">{{country}}</option>
            </select>
            <h6 class="filter-label">Select Category</h6>
            <select  class="form-control" id="exampleFormControlSelect1" v-model="category">
            <option value="" selected disabled hidden>Category</option>
            <option v-for="category in categories" v-bind:key="category.id" :value="category">{{category}} </option>
            </select>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" data-dismiss="modal" @click="PassFilters">Select</button>
      </div>
    </div>
  </div>
</div>
</template>
<script>
export default {
    data(){
        return {
            country: "",
            category: "",
             //Since we dont establish a database connection the available countries will be hard coded..
            countries: [
               "Gr","Us","Gb","Ru"
            ],
             //Since we dont establish a database connection the available categories will be hard coded..
            categories: [
                "general" ,"health", "science","sports","technology"
            ]
        }
    },
    methods: {
        PassFilters: function() {
            this.$emit('getfilters',{'country':this.country, 'category':this.category});
          
        }
    }
}
</script>
<style>
  .filter-label {
      text-align: left;
  }
  
 
 
</style>