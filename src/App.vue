<template>
  <main :class="[$style.main, $style.appContainer]">
    <AForm @addProduct="addProduct"/>
    <AProducts :list="productsList" :sorting="sortingValue" @deleteProduct="deleteProduct" @changeSort="changeSortType" />
  </main>
  <APreloader v-if="showLoader" />
</template>

<script>
import { ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'
import AForm from './components/AForm.vue'
import AProducts from './components/AProducts.vue'
import APreloader from './components/Preloader.vue'
export default {
  name: 'App',
  components: { AForm, AProducts, APreloader },
  setup() {
    let showLoader = ref(true)
    let productsList = ref([
      {id:1,name:'ЯНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzF8fGNhdHN8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60", price: '10 000'},
      {id:2,name:'ВНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1526674183561-4bfb419ab4e5?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NDB8fGNhdHN8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60", price: '14 000'},
      {id:3,name:'АНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1597850598046-28940c7ec443?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTg1fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '12 000'},
      {id:4,name:'СНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1559564207-09c99dc78a70?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTg0fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '15 000'},
      {id:5,name:'ЖНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://images.unsplash.com/photo-1481139024422-2e4ce2f87975?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTc1fHxjYXRzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60", price: '11 000'},
      {id:6,name:'УНаименование товара', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link:"https://media.istockphoto.com/photos/woman-stroking-funny-curious-young-red-ginger-maine-coon-kitten-cat-picture-id1250931010?b=1&k=20&m=1250931010&s=170667a&w=0&h=2yPHzxOSCcLfwQP23HyHm_NRL6FSI9dnDITqXvF5mXo=", price: '13 000'},
    ])
    let sortingValue = ref('')

    function changeSortType(type) {
      sortingValue.value = type
    }

    function checkStorage() {
      if(localStorage.getItem('productsList')) {
        productsList.value = JSON.parse(localStorage.getItem('productsList'))
      }
    }

    function addProduct(newProduct) {
      productsList.value.push(newProduct)
      sortProductsa(sortingValue.value)
      localStorage.setItem('productsList', JSON.stringify(productsList.value))
    }

    function deleteProduct(productId) {
      productsList.value = productsList.value.filter(prod => prod.id !== productId)
      localStorage.setItem('productsList', JSON.stringify(productsList.value))
    }

    function sortProductsa(type) {
      const copy = [...productsList.value]
      switch(type) {
        case 'priceMin':
          copy.sort((a, b) => {
            const price1 = parseInt(a.price.replace(/\s/g, ' '))
            const price2 = parseInt(b.price.replace(/\s/g, ' '))
            return price1 > price2 ? 1 : -1
          })
          break;
        case 'priceMax': 
          copy.sort((a, b) => {
            const price1 = parseInt(a.price.replace(/\s/g, ' '))
            const price2 = parseInt(b.price.replace(/\s/g, ' '))
            return price2 > price1 ? 1 : -1
          })
          break;
        case 'name':
          copy.sort((a, b) => { return a.name > b.name ? 1 : -1})
          break;
      }
      productsList.value = copy
    }

    watch(sortingValue, () => sortProductsa(sortingValue.value))

    setTimeout(() => {
      showLoader.value = false
    },1000)

    checkStorage()

    return {
      addProduct,
      productsList,
      deleteProduct,
      showLoader,
      changeSortType,
      sortingValue
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
