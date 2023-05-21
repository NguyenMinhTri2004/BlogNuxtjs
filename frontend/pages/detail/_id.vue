<template>
    <div class="d-flex flex-column justify-content-center align-items-center mt-5 " >
        <img class = "w-50" :src = "background"/>
        <p class = "w-50"  >{{blog.data?.attributes.Content}}</p>
    </div>
</template>



<script>

  export default {

    data() {
      return {
        blog: {}
      }
    },


    watch: {
    '$route.params.id': '$fetch'
    },

    
    
    async fetch() {
      const token = await process.env.NEXT_PUBLIC_STRAPI_API_TOKEN;
      const options = { headers: { Authorization: `Bearer ${token}` } };

      const local = await process.env.NEXT_STRAPI_API_URL

      const id = this.$route.params.id

      this.blog = await fetch(
        `${local}/api/blogs/${id}?populate=Image`
      ,  options).then(res => res.json())

      console.log(this.blog.data)
    },

    fetchOnServer: true,

    
    computed: {
        background(){
        return `http://localhost:1337${this.blog.data?.attributes.Image.data.attributes.formats.medium.url}`
    },
   }
} 
</script>