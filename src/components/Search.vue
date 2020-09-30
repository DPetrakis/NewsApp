<template>
     <div class="container">
    <br/>
	<div class="row justify-content-center">
                        <div class="col-12 col-md-10 col-lg-8">
                            <form class="card card-sm">
                                <div class="card-body row no-gutters align-items-center">
                                    <div class="col-auto">
                                        <i class="fas fa-search h4 text-body"></i>
                                    </div>
                                    <!--end of col-->
                                    <div class="col">
                                        <input id="Searchbar" class="form-control form-control-lg form-control-borderless" 
                                        type="search" placeholder="You can also search news only by keywords.."
                                        v-model="keyword" @keypress="PassData"
                                        >
                                    </div>
                                   
                                </div>
                            </form>
                        </div>
                        <!--end of col-->
                    </div>
</div>
</template>
<script>
export default {
    data() {
        
        return {
            keyword: ""
        };
    },
    methods: {
        PassData: function(){
          this.$emit('changemessage',this.keyword);
        }
    }
   
    
   
}
</script>
<style>
  @media (min-width: 320px) and (max-width: 480px) {
      
      #Searchbar {
          font-size: 9px;
      }   
   }
  
</style>