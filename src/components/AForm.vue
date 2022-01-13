<template>
  <div :class="$style.wrapper">
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
  </div>
</template>

<script>
import { computed, reactive, toRef } from '@vue/reactivity'
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

    return {
      inputs,
      isActive,
      buttonClass,
      formData
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
</style>
