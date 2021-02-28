<template>
  <div class="blogs">
      <h2>{{ blogTitle }}</h2>
      <input type="text" v-model="searchTerm">
      <div v-for="post in filteredPosts" :key="post.id">
         <h2>{{ post.title }}</h2> 
         <p>{{ post.body | snipet }}</p>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Blogs',
    data() {
        return {
            blogTitle: 'Blogs',
            posts: [],
            searchTerm: ''
        }
    },
    methods: {
      
    },
    computed: {
        filteredPosts() {
            return this.posts.filter(post => {
                return post.title.match(this.searchTerm)
            })
        }
    },
    created() {
        axios.get('')
       .then(response => {
           console.log(response)
           this.posts = response.data
       }).catch(err => {
           console.log(err)
       })
    },
 
}
</script>

<style>

</style>