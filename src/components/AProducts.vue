<template>
  <div :class="$style.products">
    <div :style="{'display':'flex'}">
      <button :class="$style.sortBtn">
        По умолчанию
        <img :style="{'marginLeft': '2px'}" src="@/assets/images/arrow.png">
      </button>
    </div>
    <div :class="$style.productsList">
      <AProductsCard v-for="item in list" :key="item.id" :productInfo="item"/>
    </div>
  </div>
</template>

<script>
import AProductsCard from './AProductsCard.vue'
export default {
  name: 'AProducts',
  components: { AProductsCard },
  props: {
    list: {
      type: Array,
      required: true
    }
  }
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
  
  @media screen and (max-width: 1170px) {
    .productsList {
      grid-template-columns: repeat(2, auto);
    }
  }
  @media screen and (max-width: 830px) {
    .productsList {
      grid-template-columns: repeat(1, auto);
    }
  }
  @media screen and (max-width: 640px) {
    .productsList {
      grid-template-columns: repeat(2, auto);
    }
  }
  @media screen and (max-width: 535px) {
    .productsList {
      grid-template-columns: repeat(1, auto);
    }
  }
</style>