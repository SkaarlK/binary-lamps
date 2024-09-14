<template>
    <div class="lamp-container">
      <div :class="['lamp', { on: isOn }]"></div>
      <span class="label">{{ label }}</span>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, PropType } from 'vue';
  
  export default defineComponent({
    name: 'Lamp',
    props: {
      isOn: {
        type: Boolean as PropType<boolean>,
        required: true,
      },
      label: {
        type: String as PropType<string>,
        required: true,
      },
    },
  });
  </script>
  
  <style scoped>
  .lamp-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 5px;
  }
  .lamp {
    width: 50px;
    height: 50px;
    background-color: grey;
    border-radius: 50%;
    transition: background-color 0.3s;
  }
  .lamp.on {
    background-color: yellow;
  }
  .label {
    margin-top: 5px;
    font-size: 14px;
  }
  </style>
  