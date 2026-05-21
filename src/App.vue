<script setup>
  import Navbar from './components/Navbar.vue'
  import Landing from './components/Landing.vue'
  import Projects from './components/Projects.vue'
  import Tools from './components/Tools.vue'
  import Contact from './components/Contact.vue'
  import BottomNav from './components/BottomNav.vue'
  import Footer from './components/Footer.vue'
</script>

<template>
  <Navbar/>
  <main class="container-xxl px-4 pb-5 mx-auto" >
    <Landing/>
    <Projects/>
    <Tools/>
    <Contact/>
  </main>
  <BottomNav/>
  <Footer/>
</template>
