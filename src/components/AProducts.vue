<template>
  <div :class="$style.products">
    <div :style="{'display':'flex'}">
      <div :class="$style.sortBtn" @click="sortOptionsOpen = true">
        <div>По умолчанию <img :style="{'marginLeft': '2px'}" src="@/assets/images/arrow.png"></div>
        <ul :class="$style.sortList" v-if="sortOptionsOpen" @click.stop="sortOptionsOpen = false">
          <li :class="$style.sortOption" @click="$emit('sortProducts', 'priceMin')">По цене(вниз)</li>
          <li :class="$style.sortOption" @click="$emit('sortProducts', 'priceMax')">По цене(вверх)</li>
          <li :class="$style.sortOption" @click="$emit('sortProducts', 'name')">По наименованию</li>
        </ul>
      </div>
      <div v-if="sortOptionsOpen" :class="$style.sortOpenBg" @click="sortOptionsOpen = false"></div>
    </div>
    <div :class="$style.productsList">
      <transition-group
        enter-active-class="animate__animated animate__slideInDown"
        leave-active-class="animate__animated animate__slideOutUp"
      >
        <AProductsCard v-for="item in list" :key="item.id" :productInfo="item" @delete="deleteOneProduct"/>
      </transition-group>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import AProductsCard from './AProductsCard.vue'
export default {
  name: 'AProducts',
  components: { AProductsCard },
  emits: ['deleteProduct', 'sortProducts', 'listLoaded'],
  props: {
    list: {
      type: Array,
      required: true
    }
  },
  setup(props, { emit }) {
    function deleteOneProduct(id) {
      emit('deleteProduct', id)
    }
    let sortOptionsOpen = ref(false)

    return { deleteOneProduct, sortOptionsOpen }
  }
}
</script>

<style module>
  .sortOpenBg {
    top: 0;bottom: 0; left: 0; right: 0;
    position: absolute;
    z-index: 2;
  }
  .sortList {
    position: absolute;
    box-shadow: var(--shadow-product);
    background-color: rgb(255, 254, 251);
    padding: 5px 16px 5px;
    left: 0;
    top: 40px;
    border-radius: var(--radius-sm);
    z-index: 3;
  }
  .sortOption {
    color: var(--color-primary);
  }
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
    background-color: #FFFEFB;
    z-index: 3;
    position: relative;
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