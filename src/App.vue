<template>
  <div id="app">
    <!-- <add-blog></add-blog> -->
    <!-- <show-blogs></show-blogs>
    <list-Blogs></list-Blogs> -->
    <app-header></app-header>
    <router-view></router-view>
  </div>
</template>

<script>
import addBlog from './components/addBlog.vue'
import showBlogs from './components/showBlogs.vue'
import listBlogs from './components/listBlogs.vue'
import header from './components/header.vue'

export default {
  components: {
    'add-blog': addBlog,
    'show-blogs': showBlogs,
    'list-Blogs': listBlogs,
    'app-header': header
  },
  data () {
    return {
    }
  }
}
</script>

<style>
body{
  margin: 0;
  font-family: 'Nunito SemiBold';
}

</style>
