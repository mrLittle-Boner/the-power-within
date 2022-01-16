<template>
  <main :class="[$style.main, $style.appContainer]">
    <AForm @addProduct="addProduct"/>
    <AProducts :list="productsList" />
  </main>
</template>

<script>
import { reactive } from '@vue/reactivity'
import AForm from './components/AForm.vue'
import AProducts from './components/AProducts.vue'
export default {
  name: 'App',
  components: { AForm, AProducts },
  setup() {

    let productsList = reactive([
      {id:1,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzF8fGNhdHN8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60", price: '10 000'},
      {id:2,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1526674183561-4bfb419ab4e5?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NDB8fGNhdHN8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60", price: '14 000'},
      {id:3,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1597850598046-28940c7ec443?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTg1fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '12 000'},
      {id:4,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1559564207-09c99dc78a70?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTg0fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '15 000'},
      {id:5,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1481139024422-2e4ce2f87975?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTc1fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '11 000'},
      {id:6,name:'Наименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://media.istockphoto.com/photos/woman-stroking-funny-curious-young-red-ginger-maine-coon-kitten-cat-picture-id1250931010?b=1&k=20&m=1250931010&s=170667a&w=0&h=2yPHzxOSCcLfwQP23HyHm_NRL6FSI9dnDITqXvF5mXo=", price: '13 000'},
    ])

    function addProduct(newProduct) {
      productsList.push(newProduct)
    }


    return {
      addProduct,
      productsList
    }
  }
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
