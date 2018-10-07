<template>
  <div class="container">
    <header>
      <h1 class="heading">
        Welcome,
        <br>
        This website was made to practice Vue and vue-resource
      </h1>

      <p>Check out these links below:</p>
      <ul>
        <li v-for="link in links"><a v-bind:href="link.src">{{ link.title }}</a></li>
      </ul>
    </header>
    <main>
      <appForm></appForm>
    </main>
    <footer>
      <p>&copy; Vue is cool 2018</p>
    </footer>
  </div>
</template>

<script>
import appForm from './components/new-blog'
import blogs from './components/blogs'

export default {
  components: {
    appForm: appForm,
    blogs: blogs
  },
  data() {
      return {
      component: 'blogs',
      links: [
        {src: 'https://planeswalker1.github.io/', title: 'My Website'},
        {src: 'https://colorlessenergy.github.io/', title: 'Cool Website'},
        {src: 'https://github.com/planeswalker1', title: 'My Github'},
        {src: 'https://github.com/colorlessenergy', title: 'Cool Github'},
      ],
      components: [
        {name: 'blogs', title: 'All Blogs'},
        {name: 'appForm', title: 'New Blog'},
      ],
      };
    }
  }
</script>

<style>
  html {
    box-sizing: border-box;
  }

  *,
  *:before,
  *:after {
    box-sizing: inherit;
  }

  body {
    font-family: sans-serif;
    margin: 0;
  }

  .container {
    margin: 0 auto;
    max-width: 1360px;
    width: 50%;
  }

  /* link styles */
  ul {
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
    padding: 0;
    width: 100%;
  }

  li {
    margin-right: 10px;
  }

  a {
    background-color: transparent;
    color: #007bff;
    text-decoration: none;
  }

  a:hover {
    color: #0056b3;
    text-decoration: underline;
  }

  footer {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  @media screen and (max-width: 800px) {
    .container {
      padding: 20px;
      width: 80%;
    }

    input,
    textarea {
      width: 100%;
    }
  }

  @media screen and (max-width: 500px) {
    .container {
      padding: 10px;
      width: 90%;
    }
  }
</style>
