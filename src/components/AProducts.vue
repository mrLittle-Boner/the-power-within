<template>
  <div :class="$style.products">
    <div :style="{'display':'flex'}">
      <button :class="$style.sortBtn">
        По умолчанию
        <img :style="{'marginLeft': '2px'}" src="@/assets/images/arrow.png">
      </button>
    </div>
    <div :class="$style.productsList">
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
      <AProductsCard />
    </div>
  </div>
</template>

<script>
import AProductsCard from './AProductsCard.vue'
export default {
  name: 'AProducts',
  components: { AProductsCard }
}
</script>

<style module>
  .products {
    color: var(--color-primary);
    width: 100%;
  }
  .productsList {
    display: grid;
    grid-template-columns: repeat(3, minmax(auto,332px));
    gap: var(--space-sm);
  }
  .sortBtn {
    margin-bottom: var(--space-sm);
    color: var(--color-grey);
    border-radius: var(--radius-sm);
    box-shadow: var(--shadow-input);
    font-size: 1.2rem;
    padding: 10px 16px 11px;
    margin-left: auto;
    cursor: pointer;
    background-color: #FFFEFB;;
  }
</style>