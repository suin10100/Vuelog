<template>
  <div id="app">
    <div id="add-blog">
      <h2>Add a new Blog Post</h2>
      <form v-if="!submitted">
        <label>Blog Title:</label>
        <input type="text" v-model="blog.title" required />
        <label>Blog Content:</label>
        <textarea v-model.lazy="blog.content"></textarea>
        <!-- v-model.lazy 양뱡항 바인딩 수행... -->
        <!-- https://kkh0977.tistory.com/2288 -->
        <label>Name:</label>
        <textarea v-model.lazy="blog.userId"></textarea>
        <div id="checkboxes">
          <label>Ninjas</label>
          <input type="checkbox" value="ninjas" v-model="blog.categories" />
          <label>Wizards</label>
          <input type="checkbox" value="wizards" v-model="blog.categories" />
          <label>Mario</label>
          <input type="checkbox" value="Mario" v-model="blog.categories" />
          <label>Cheese</label>
          <input type="checkbox" value="cheese" v-model="blog.categories" />
        </div>
        <label>Author:</label>
        <select v-model="blog.author">
          <option v-for="author in authors">{{ author }}</option>
        </select>
        <hr />
        <button v-on:click.prevent="post">Add Blog</button>
        <!-- event modifier -->
      </form>
      <div v-if="submitted">
        <h3>Thanks for adding your post</h3>
      </div>
      <div id="preview">
        <h3>Preview Blog</h3>
        <p>Blog title: {{ blog.title }}</p>
        <p>Blog content:</p>
        <p>{{ blog.content }}</p>
        <p>Blog categories:</p>
        <!-- <ui> -->
        <li v-for="category in blog.categories">{{ category }}</li>
        <!-- </ui> -->
        <p>Author: {{ blog.author }}</p>
        <p>Id: {{ blog.userId }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
        userId: ""
      },
      authors: ["The Net Ninja", "The Angular Ave", "person3"],
      submitted: false
    };
  },
  methods: {
    post: function() {
      this.$http
        .post(
          "https://vuejs-practice-7bdb9-default-rtdb.firebaseio.com/posts.json",
          this.blog
        )
        .then(function(data) {
          console.log(data);
          this.submitted = true;
        });
    }
  }
};
</script>

<style>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label {
  display: inline-block;
}
</style>
