<template>
  <div>
    <b-container class="mt-3">
      <b-carousel id="carousel-fade" style="text-shadow: 0px 0px 2px #000" fade indicators img-width="1024" img-height="300">
        <b-carousel-slide v-for="slider in sliders" :key="slider.id" :img-src="slider.image"></b-carousel-slide>
      </b-carousel>
    </b-container>
  </div>
</template>

<script>
  export default {
  
    //data function
    data() {
      return {
        //state sliders
        sliders: []
      }
    },

    async fetch() {

      //fething sliders on Rest API
      await this.$axios.get('/api/web/sliders')
      .then(response => {

        //assign response to state "sliders"
        this.sliders = response.data.data
      })
    }
    
  }
</script>