<template>
  <div :class="[$style.card, isSelected && $style.selected]" @click="toggleSelect">
    <div :class="$style.imageWrapper">
      <img :class="$style.image" src="@/assets/images/product-photo.jpg" alt="photo of the product">
    </div>
    <div :class="$style.info">
      <h3 :class="$style.title">Наименование товара</h3>
      <p :class="$style.description"> Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк</p>
      <div :class="$style.price">10 000 руб.</div>
    </div>
    <button v-if="isSelected" :class="$style.deleteBtn">
      <img src="@/assets/images/delete-btn.png" alt="delete item from the list">
    </button>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
  name: 'AProductsCard',
  setup(){
    const isSelected = ref(false)

    function toggleSelect() {
      isSelected.value = !isSelected.value
    }

    return {
      isSelected,
      toggleSelect
    }
  }
}
</script>


<style module>
.card{
  box-shadow: var(--shadow-product);
  cursor: pointer;
  position: relative;
  border-radius: var(--radius-sm);
  transition: all .3s ease;
}
.selected {
  outline: 1px solid #7BAE73;
}
.card:hover {
  transform: scale(1.02);
}
.imageWrapper{
  font-size: 0;
  border-top-left-radius: var(--radius-sm);
  border-top-right-radius: var(--radius-sm);
  overflow: hidden;
}
.image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}
.info {
  padding: var(--space-sm);
  padding-bottom: var(--space-m);
}
.title {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: var(--space-sm);
}
.description {
  margin-bottom: var(--space-lg);
}
.price {
  font-size: 2.4rem;
  font-weight: 600;
}
.deleteBtn {
  font-size: 0;
  position: absolute;
  background-color: tomato;
  padding: 8px;
  top: -8px;
  right: -8px;
  border-radius: var(--radius-lg);
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

</style>