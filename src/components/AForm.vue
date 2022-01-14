<template>
  <div :class="$style.wrapper" v-show="isOpen">
    <h3 :class="$style.heading">Добавление товара</h3>
    <form :class="$style.form">
      <AFormInput
        v-for="(input,index) in inputs" :key="index"
        :class="$style.formInput"
        :htmlTag="input.htmlTag"
        :title="input.title"
        :placeholder="input.placeholder"
        :isRequired="input.isRequired"
        v-model="input.model.value"
      />
      <button :class="[$style.formBtn, $style[buttonClass]]" :disabled="!isActive">Добавить товар</button>
    </form>
    <button @click="hideForm" :class="$style.mobileClose">+</button>
    <teleport to='main'>
      <button v-if="mobileView" @click="showForm" :class="$style.mobileFormShow">Добавление товара</button>
    </teleport>
  </div>
</template>

<script>
import { computed, reactive, ref, toRef } from '@vue/reactivity'
import AFormInput from './AFormInput.vue'
export default {
  name: 'AForm',
  components: { AFormInput },
  setup() {
    const defaultFormData = {
      name: '',
      description: '',
      link: '',
      price: ''
    }
    const isActive = false
    const buttonClass = computed(() => {
      return isActive ? 'formBtn--active' : 'formBtn--disabled'
    })
    
    const formData = reactive(defaultFormData)
    const inputs = [
      {
        htmlTag:'input',
        title: 'Наименование Товара',
        placeholder: 'Введите наименование товара',
        model: toRef(formData, 'name'),
        isRequired: true
      },
      {
        htmlTag:'textarea',
        title: 'Описание товара',
        placeholder: 'Введите описание товара',
        model: toRef(formData, 'description'),
        isRequired: false
      },
      {
        htmlTag:'input',
        title: 'Ссылка на изображение товара',
        placeholder: 'Введите ссылку',
        model: toRef(formData, 'link'),
        isRequired: true
      },
      {
        htmlTag:'input',
        title: 'Цена товара',
        placeholder: 'Введите цену',
        model: toRef(formData, 'price'),
        isRequired: true
      }
    ]

    const isOpen = ref(false)
    const mobileView = ref(false)

    function hideForm() {
      isOpen.value = false
    }
    function showForm() {
      isOpen.value = true
    }

    window.addEventListener('resize', () => {
      if(window.innerWidth >= 640) {
        isOpen.value = true
        mobileView.value = false
      }
      if(window.innerWidth <= 640) {
        isOpen.value = false
        mobileView.value = true
      }
    })

    return {
      inputs,
      isActive,
      buttonClass,
      formData,
      isOpen,
      mobileView,
      hideForm,
      showForm
    }
  }
}
</script>


<style module>
  .formInput:not(:last-of-type) {
    margin-bottom: var(--space-sm);
  }
  .formInput:last-of-type {
    margin-bottom: var(--space-m);
  }
  .wrapper {
    width: 332px;
    flex-shrink: 0;
  }
  .heading {
    font-size: 28px;
    margin-bottom: var(--space-sm);
    color: var(--color-primary);
  }
  .form {
    box-shadow: var(--shadow-product);
    padding: var(--space-m);
    border-radius: var(--radius-sm);
    position: sticky;
    top: var(--space-m);
  }
  .formBtn {
    width: 100%;
    padding: 10px 0 11px;
    font-size: 12px;
    border-radius: var(--radius-lg);
    cursor: pointer;
  }
  .formBtn--active {
    background-color: #7BAE73;
    box-shadow: var(--shadow-input);
    color: #fff;
  }
  .formBtn--disabled {
    background-color: #eee;
    color: var(--color-grey);
    cursor: not-allowed;
  }

  .mobileClose {
    position: absolute;
    top: 10px;
    right: 20px;
    line-height: 1;
    color: crimson;
    font-weight: bold;
    font-size: 3rem;
    background: transparent;
    transform: rotate(45deg);
  }
  .mobileFormShow {
    position: fixed;
    background-color: #7BAE73;
    color: #fff;
    border-radius: 15px 15px 0 0;
    padding: 4px 8px;
    transform: rotate(90deg);
    left: -63px;
    top: 40%;
  }
  
  @media screen and (max-width: 950px) {
    .wrapper {
      width: 270px;
    }
    .form {
      padding-right: var(--space-sm);
      padding-left: var(--space-sm);
    }
  }
  @media screen and (max-width: 640px) {
    .wrapper {
      width: 100%;
      position: fixed;
      background-color: #fff;
      z-index: 42;
      top: 0;
      left: 0;
      bottom: 0;
      padding-top: var(--space-lg);
    }
    .form {
      position: relative;
      top: 0;
      box-shadow: none;
    }
    .heading {
      text-align: center;
    }
    .formBtn {
      font-size: 1.8rem;
    }
  }
</style>
