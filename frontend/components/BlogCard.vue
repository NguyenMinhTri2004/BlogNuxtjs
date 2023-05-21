<template>
  <div>
    <b-card
      :title= data.attributes.Title
      :img-src= "background"
      img-alt="Image"
      img-top
      tag="article"
      class = "w-100 h-100"
    >
      <b-card-text>
          {{data.attributes.Des}}
      </b-card-text>

     
      
          <nuxt-link :to= "`detail/${data.id}`">
              Xem chi tiet
          </nuxt-link>
       
    </b-card>
  </div>
</template>


<script>
    
  export default {
      computed: {
        background(){
        return `http://localhost:1337${this.data.attributes.Image.data.attributes.formats.medium.url}`
    },
  },

    props: ['data'],
  }
</script>


