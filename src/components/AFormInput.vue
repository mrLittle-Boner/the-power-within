<template>
  <label :class="$style.label">
    <span :class="[$style.title, isRequired && $style.required]">{{ title }}</span>

    <input 
      v-if="htmlTag === 'input'" 
      :type="inputType" 
      :class="$style.input" 
      :placeholder="placeholder"
      :required="isRequired"
      v-model="value"
    >

    <textarea 
      v-if="htmlTag === 'textarea'" 
      :class="[$style.input, $style.textarea]"
      :placeholder="placeholder"
      :required="isRequired"
      v-model="value"
    ></textarea>

  </label>
</template>

<script>
import { computed } from '@vue/reactivity'
export default {
  props:{
    modelValue: {
      type: String,
      required: true
    },
    htmlTag: {
      type: String,
      default: () =>'input'
    },
    inputType: {
      type: String,
      default: () => 'text'
    },
    title: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      default: () => 'Введите значeние'
    },
    isRequired: {
      type: Boolean,
      default: () => false
    }
  },
  emits: ['update:modelValue'],
  setup(props, {emit}) {
    const value = computed({
      get(){return props.modelValue},
      set(value){ emit('update:modelValue', value)}
    })
    return {value}
  },
}
</script>

<style module>
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

  .textarea {
    resize: none;
    height: 108px;
  }
  @media screen and (max-width: 640px) {
    .title,
    .input,
    .input::placeholder {
      font-size: 1.6rem;
    }
  }
</style>