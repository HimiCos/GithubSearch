<template>
  <div class="container">
    <ComSearch/>
    <ComList/>
  </div>
</template>

<script>
  import ComSearch from './components/ComSearch';
  import ComList from './components/ComList';

  export default {
    name: "App",
    components: { ComSearch, ComList }
  };
</script>
<style>
*{
  margin: 10px 0px;
}
</style>