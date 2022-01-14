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
  gap: var(--space-sm);
  padding: var(--space-lg);
  position: relative;
}
.appContainer {
  max-width: 1440px;
  margin: 0 auto;
  width: 100%;
  min-height: 100vh;
}

@media screen and (max-width: 1170px) {
  .main {
    padding-right:var(--space-sm);
    padding-left:var(--space-sm);
  }
}
</style>
