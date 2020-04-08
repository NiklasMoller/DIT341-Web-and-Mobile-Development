<template>
  <div id="app">
    <NavBar></NavBar>

    <router-view/>
  </div>
</template>

<style>
  @import 'assets/css/stylesheet.css';



</style>

<script>

    import DropdownMenu from './components/DropdownMenu'
    import NavBar from './components/NavBar'
    export default {
        name: 'app',
        components: {
            'DropdownMenu': DropdownMenu,
            'NavBar': NavBar
        }
    }


</script>
