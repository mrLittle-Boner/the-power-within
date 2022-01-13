<template>
  <main :class="[$style.main, $style.appContainer]">
    <AForm />
    <AProducts />
  </main>
</template>

<script>
import AForm from './components/AForm.vue'
import AProducts from './components/AProducts.vue'
export default {
  name: 'App',
  components: { AForm, AProducts }
}
</script>

<style module>
.main {
  display: flex;
  padding: var(--space-lg);
}
.appContainer {
  max-width: 1440px;
  margin: 0 auto;
  width: 100%;
  min-height: 100vh;
}

</style>
