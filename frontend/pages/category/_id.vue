<template>
    <div class="w-100 d-flex flex-row flex-wrap align-items-center justify-content-center mt-5" >
      <div class = "w-25 mx-auto " :key="blog.id" v-for="blog of blogs"> 
        <BlogCard :data=blog />
      </div>
    </div>
  </template>

  
  <script>

  
    import BlogCard from '../../components/BlogCard.vue';
  
    export default {
  
      data() {
        return {
          blogs: []
        }
      },
  
  
      watch: {
      '$route.params.id': '$fetch'
      },
  
     
      async fetch() {
        const token = await process.env.NEXT_PUBLIC_STRAPI_API_TOKEN;
        const options = { headers: { Authorization: `Bearer ${token}` } };
  
        const local = await process.env.NEXT_STRAPI_API_URL
  
        const tmp = await fetch(
          `${local}/api/blogs?populate=*`
        ,  options).then(res => res.json())



        this.blogs = tmp.data.filter(item => item.attributes.type.data.id === parseInt(this.$route.params.id))
  
       
      },
  
  
      fetchOnServer: true,
  
      components: {
             BlogCard
      }
    }
  </script>