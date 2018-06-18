<template>
  <div>
    <header-component></header-component>
    <div class="wrapper">
      <Sidebar></Sidebar>
      <Content></Content>
    </div>
    <footer-component></footer-component>
  </div>
</template>

<script>
  import Content from './content/Content';
  import Sidebar from './sidebar/Sidebar';
  import HeaderComponent from './header/Header';
  import FooterComponent from './footer/Footer';

  export default {
    name: "index",
    components: {
      Sidebar,
      Content,
      HeaderComponent,
      FooterComponent,
    }
  }
</script>

<style scoped>

</style>
