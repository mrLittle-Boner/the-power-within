<template>
  <div :class="$style.wrapper" v-show="isOpen">
    <h3 :class="$style.heading">Добавление товара</h3>
    <form :class="$style.form">
      <label :class="$style.label">
        <span :class="[$style.title, $style.required]">Наименование товара</span>
        <input 
          type="text"
          :class="[$style.input, v$.name.$error && $style.error]" 
          placeholder="Введите наименование товара"
          v-model.trim="name"
          @blur="v$.name.$touch"
          required
        >
        <div v-if="v$.name.$error" :class="$style.errorMessage">Поле является обязательным</div>
      </label>

      <label :class="$style.label">
        <span :class="[$style.title, $style.required]">"Описание товара</span>
        <textarea 
          :class="[$style.input, $style.description]"
          placeholder="Введите Описание товара"
          v-model="description"
        ></textarea>
      </label>

      <label :class="$style.label">
        <span :class="[$style.title, $style.required]">Ссылка на изображение товара</span>
        <input 
          type="url"
          :class="[$style.input, v$.link.$error && $style.error]" 
          placeholder="Введите ссылку"
          v-model.trim="link"
          @blur="v$.link.$touch"
          required
        >
        <div v-if="v$.link.$error" :class="$style.errorMessage">Поле является обязательным</div>
      </label>

      <label :class="$style.label">
        <span :class="[$style.title, $style.required]">Цена товара</span>
        <input 
          type="number"
          :class="[$style.input, v$.price.$error && $style.error]" 
          placeholder="Введите цену"
          v-model.trim="price"
          @blur="v$.price.$touch"
          required
        >
        <div v-if="v$.price.$error" :class="$style.errorMessage">Поле является обязательным</div>
      </label>

      <button :class="[$style.formBtn, isFromButtonActive ? $style.formBtnActive : $style.formBtnDisabled]" 
        :disabled="!isFromButtonActive">
        Добавить товар
      </button>
    </form>
  
    <button @click="isOpen = false" :class="$style.mobileClose">+</button>
  
    <teleport to='body'>
      <button v-if="!isOpen" @click="isOpen = true" :class="$style.mobileFormShow">Добавление товара</button>
    </teleport>

  </div>
</template>

<script>
import { computed, reactive, toRefs, ref } from '@vue/reactivity'
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'

export default {
  name: 'AForm',
  setup() {
    const formData = reactive({
      name: '',
      description: '',
      link: '',
      price: null
    })

    const rules = {
      name: { required },
      link: { required },
      price: { required }
    }

    const v$ = useVuelidate(rules, formData)

    const isFromButtonActive = computed(() => {
      const { name, link, price } = formData
      return Boolean(name && link && price) && v$.value.$errors.length === 0
    })

    const isOpen = ref(null)
    window.innerWidth <= 640 ? isOpen.value = false : isOpen.value = true

    window.addEventListener('resize', () => {
      if(window.innerWidth >= 640) {
        isOpen.value = true
      }
      if(window.innerWidth <= 640) {
        isOpen.value = false
      }
    })

    return {
      ...toRefs(formData),
      isOpen,
      v$,
      isFromButtonActive,
    }
  }
}
</script>


<style module>
  .form label:not(:last-of-type) {
    margin-bottom: var(--space-sm);
  }
  .form label:last-of-type {
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
  .formBtnActive {
    background-color: #7BAE73;
    box-shadow: var(--shadow-input);
    color: #fff;
  }
  .formBtnDisabled {
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

  .input {
    border-radius: var(--radius-sm);
    box-shadow: var(--shadow-input);
    padding: 10px 16px 11px;
    width: 100%;
    border: none;
    font-size: 1.2rem;
  }
  .input::placeholder {
    font-size: 1.2rem;
    color: var(--color-grey);
  }
  .error {
    outline: 1px solid #FF8484;
  }
  .description {
    resize: none;
    height: 108px;
    letter-spacing: -0.02em;
  }
    .label {  
    width: 100%;
    display: inline-block;
    font-size: 0;
  }
  .title {
    display: inline-block;
    margin-bottom: 4px;
    font-size: 1rem;
    color: var(--color-black);
    line-height: 13px;
    position: relative;
  }
  .required::after {
    content: '';
    width: 4px;
    height: 4px;
    background-color: #FF8484;
    border-radius: var(--radius-sm);
    position: absolute;
  }
  .errorMessage {
    font-size: 0.8rem;
    color: #FF8484;
    margin-top: 4px;
  }
</style>
