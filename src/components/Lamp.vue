<template>
    <div class="lamp-container" @click="toggle">
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
    emits: ['toggle'],
    methods: {
      toggle() {
        this.$emit('toggle');
      },
    },
  });
  </script>
  
  <style scoped>
  .lamp-container {
    display: flex;
    align-items: center;
    cursor: pointer;
  }
  
  .lamp {
    width: 20px;
    height: 20px;
    margin-right: 10px;
    background-color: grey;
    border-radius: 50%;
  }
  
  .lamp.on {
    background-color: yellow;
  }
  </style>
  