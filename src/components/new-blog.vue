<template>
  <div class="blog">
    <h2>Add a New Blog Post</h2>
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
  h1,
  form {
    margin: 0 auto;
    max-width: 600px;
  }

  p {
    margin-bottom: 0;
  }

  .form__header,
  .form__fields,
  .form__controls {
    padding: 5px;
  }

  /* form control styles */
  .group {
    margin-bottom: 10px;
  }

  .group__label {
    display: block;
    margin: .5em 0;
  }

  .group__input {
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: .25em;
    color: #495057;
    display: block;
    font-size: 1em;
    line-height: 1.5;
    padding: .375em .75em;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  }

  .group__input:focus {
    background-color: #fff;
    border-color: #80bdff;
    box-shadow: 0 0 0 0.2em rgba(0,123,255,.25);
    color: #495057;
    outline: 0;
  }

  .group__textarea {
    background-clip: padding-box;
    background-color: #fff;
    border: 1px solid #ced4da;
    border-radius: .25em;
    color: #495057;
    display: block;
    line-height: 1.5;
    overflow: auto;
    padding: .375em .75em;
    resize: vertical;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  }

  .group__textarea:focus {
    background-color: #fff;
    border-color: #80bdff;
    box-shadow: 0 0 0 0.2em rgba(0,123,255,.25);
    color: #495057;
    outline: 0;
  }

  .group__input,
  .group__textarea {
    width: 100%;
  }

  .btn {
    background-color: #007bff;
    border: 1px solid transparent;
    border-color: #007bff;
    border-radius: .25em;
    color: #fff;
    display: inline-block;
    font-size: 1em;
    font-weight: 400;
    line-height: 1.5;
    padding: .375em .75em;
    text-align: center;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    user-select: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    vertical-align: middle;
    white-space: nowrap;
  }

  .btn:hover {
    background-color: #0069d9;
    border-color: #0062cc;
    color: #fff;
    cursor: pointer;
  }

  .btn:focus {
    outline: 0;
    box-shadow: 0 0 0 0.2em rgba(0,123,255,.5);
  }

  .preview {
    border: 1px dotted #ccc;
    margin: 30px 0;
    padding: 10px 20px;
  }

  /* radio button styles */
  .checkbox,
  .selectbox {
    margin: 10px 0;
  }

  /* The container */
  .radio {
      cursor: pointer;
      display: inline-block;
      margin: 10px;
      padding-left: 25px;
      position: relative;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
  }

  /* Hide the browser's default checkbox */
  .radio .radio__checkbox {
      display: none;
      /* cursor: pointer;
      opacity: 0;
      position: absolute; */
  }

  /* Create a custom checkbox */
  .radio__checkmark {
      background-color: #eee;
      height: 17px;
      position: absolute;
      top: 0;
      left: 0;
      width: 17px;
  }

  /* On mouse-over, add a grey background color */
  .radio:hover .radio__checkbox ~ .radio__checkmark {
      background-color: #ccc;
  }

  /* When the checkbox is checked, add a blue background */
  .radio .radio__checkbox:checked ~ .radio__checkmark {
      background-color: #007bff;
  }

  /* Create the checkmark/indicator (hidden when not checked) */
  .radio__checkmark:after {
      content: "";
      display: none;
      position: absolute;
  }

  /* Show the checkmark when checked */
  .radio__checkbox:checked ~ .radio__checkmark:after {
      display: block;
  }

  /* Style the checkmark/indicator */
  .radio__checkmark:after {
      border: solid white;
      border-width: 0 3px 3px 0;
      height: 10px;
      top: 3px;
      left: 6px;
      -webkit-transform: rotate(45deg);
      -ms-transform: rotate(45deg);
      transform: rotate(45deg);
      width: 5px;
  }

  /* select input styles */
  .select {
    -moz-appearance: none;
    -webkit-appearance: none;
    background: #fff url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 4 5'%3E%3Cpath fill='%23333' d='M2 0L0 2h4zm0 5L0 3h4z'/%3E%3C/svg%3E") no-repeat right .75rem center;
    background-size: 8px 10px;
    -webkit-background-size: 8px 10px;
    border: 1px solid rgba(0,0,0,.15);
    border-radius: .25em;
    color: #464a4c;
    cursor: pointer;
    display: inline-block;
    height: calc(2.25em + 2px);
    line-height: 1.25;
    max-width: 100%;
    padding: .375rem 1.75rem .375rem .75rem;
    vertical-align: middle;
  }

  .select:focus {
    border-color: #5cb3fd;
    cursor: pointer;
    outline: 0;
  }

  .select:active {
    border-color: #5cb3fd;
    cursor: pointer;
    outline: 0;
  }

  button {
    background-color: #007bff;
    border: 1px solid transparent;
    border-color: #007bff;
    border-radius: .25em;
    color: #fff;
    display: inline-block;
    font-size: 1em;
    font-weight: 400;
    line-height: 1.5;
    padding: .375em .75em;
    text-align: center;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    user-select: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    vertical-align: middle;
    white-space: nowrap;
  }

  button:hover {
    background-color: #0069d9;
    border-color: #0062cc;
    color: #fff;
    cursor: pointer;
  }

  button:focus {
    outline: 0;
    box-shadow: 0 0 0 0.2em rgba(0,123,255,.5);
  }
</style>