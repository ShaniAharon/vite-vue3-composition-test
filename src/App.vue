<script setup lang="ts">
  import todoApp from './components/todo-app.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <todoApp />
    </div>
  </header>
</template>

<style>
  @import './assets/base.css';

  body {
    box-sizing: border-box;
  }

  #app {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;

    font-weight: normal;
  }

  header {
    line-height: 1.5;
    text-align: center;
  }

  .logo {
    display: block;
    margin: 0 auto 2rem;
  }

  a,
  .green {
    text-decoration: none;
    color: hsla(160, 100%, 37%, 1);
    transition: 0.4s;
  }

  @media (hover: hover) {
    a:hover {
      background-color: hsla(160, 100%, 37%, 0.2);
    }
  }

  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      justify-content: center;
      /* padding-right: calc(var(--section-gap) / 2); */
    }

    .logo {
      margin: 0 2rem 0 0;
    }
  }
</style>
