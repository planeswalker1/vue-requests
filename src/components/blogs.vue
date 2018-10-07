<template>
  <div class="blogs">
    <h2>All Blog Articles</h2>
    <div v-for="blog in blogs" class="blog">
      <h2>{{ blog.title }}</h2>
      <article>
        {{ blog.body }}
      </article>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        blogs: []
      };
    },
    created() {
      this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function (data) {
        console.log(data);
        this.blogs = data.body.slice(0, 10);
      });
    }
  }
</script>

<style scoped>
  .blog {
    background-color: #eee;
    border-radius: 10px;
    margin: 20px 0;
    padding: 20px;
  }
</style>