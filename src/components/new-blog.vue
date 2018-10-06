<template>
  <div class="blog">
    <h2>Add a New Blog Post</h2>
    <ul>
      <li v-for="link in links"><a v-bind:href="link.src">{{ link.name }}</a></li>
    </ul>
    <form v-on:submit.prevent="post" v-if="!submitted">
      <!-- title -->
      <div class="form__group">
        <label class="group__label" for="title"><strong>Title: </strong></label>
        <input class="group__input" v-model="blog.title" id="title" type="text">
      </div>

      <!-- text -->
      <div class="form__group">
        <label class="group__label" for="text"><strong>Text: </strong></label>
        <textarea class="group__textarea" v-model="blog.text" id="text" name="" cols="30" rows="10"></textarea>
      </div>

      <!-- categories -->
      <div class="form__group">
        <label class="group__label" for="category"><strong>Category: </strong></label>
        <div id="category" class="checkbox">
          <label class="radio" v-for="category in categories">
            {{ category }}
            <input class="radio__checkbox" type="checkbox" name="category" v-bind:value="category" v-model="blog.categories">
            <span class="radio__checkmark"></span>
          </label>
        </div>
      </div>

      <!-- author -->
      <div class="form__group">
        <div class="selectbox">
          <label class="group__label" for="author"><strong>Author: </strong></label>
          <select class="select" id="author" v-model="blog.author">
            <option selected value="">Select Author</option>
            <option v-for="author in authors" v-bind:value="author">{{ author }}</option>
          </select>
        </div>
      </div>
      <button type="submit">Add Blog</button>
    </form>

    <!-- form sent message -->
    <div v-if="submitted">
      <h3>Thanks for adding your post</h3>
    </div>

    <!-- preview -->
    <div class="preview">
      <h3>Preview Blog</h3>
      <p>Title: </p>
      <p>{{ blog.title }}</p>
      <p>Text: </p>
      <p>{{ blog.text }}</p>
      <p>Categories: </p>
      <ul class="preview__categories">
        <li v-for="category in blog.categories">{{ category }}</li>
      </ul>
      <p>Author: </p>
      <p>{{ blog.author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: {
        title: '',
        text: '',
        categories: [],
        author: ''
      },
      links: [
        {src: 'https://planeswalker1.github.io/', name: 'Home'},
        {src: 'http://colorlessenergy.github.io/', name: 'About'}
      ],
      categories: ['HTML', 'CSS', 'JavaScript', 'Other'],
      authors: ['Angel', 'Brian','Christian','Daniel', 'David'],
      submitted: false
    };
  },
  methods: {
    post: function () {
      this.$http.post('https://jsonplaceholder.typicode.com/posts', {
        title: this.blog.title,
        body: this.blog.text,
        userId: 1
      }).then(function (data) {
        console.log(data);
        this.submitted = true;
      });
    }
  }
}
</script>

<style scoped>

</style>