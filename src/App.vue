<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
});
</script>
<template>
  <router-view />
</template>

<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  body {  
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    background:darkseagreen;
  }

  canvas {
    width: 1000px;
    height: 800px;
    border-radius: 20px;
    -webkit-box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
    -moz-box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
    box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
  }

  @media only screen and (max-width: 600px) {
    * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
    }

    canvas {
      width: 400px;
      height: 500px;
      border-radius: 20px;
      -webkit-box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
      -moz-box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
      box-shadow: 8px 8px 24px 0px rgba(66, 68, 90, 1);
    }
  }
</style>
