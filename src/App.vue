<template>
  <div class="container">
    <appForm></appForm>
  </div>
</template>

<script>
import appForm from './components/new-blog'

export default {
  components: {
    appForm: appForm
  },
  data() {
      return {

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
  }
</style>
