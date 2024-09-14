<template>
  <div id="app">
    <h1>Binary Representation of {{ decimalNumber }}</h1>
    <div class="lamps">
      <Lamp v-for="(lamp, index) in lamps" :key="index" :isOn="lamp.isOn" :label="lamp.label" />
    </div>
    <input type="number" v-model.number="decimalNumber" @input="updateLamps" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Lamp from './components/Lamp.vue';

export default defineComponent({
  name: 'App',
  components: {
    Lamp,
  },
  setup() {
    const decimalNumber = ref(10);
    const lamps = ref<{ isOn: boolean; label: string }[]>([]);

    const updateLamps = () => {
      const binaryString = decimalNumber.value.toString(2).padStart(8, '0');
      lamps.value = binaryString.split('').map((bit, index) => ({
        isOn: bit === '1',
        label: `2^${7 - index} = ${2**(7-index)}`,
      }));
    };

    updateLamps();

    return {
      decimalNumber,
      lamps,
      updateLamps,
    };
  },
});
</script>

<style>
#app {
  text-align: center;
}
.lamps {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}
input {
  margin-top: 20px;
}
</style>
