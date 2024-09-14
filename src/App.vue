<template>
  <div id="app">
    <h1>Binary Representation of {{ decimalNumber }}</h1>
    <div class="lamps">
      <Lamp v-for="(lamp, index) in lamps" :key="index" :isOn="lamp.isOn" :label="lamp.label" @toggle="toggleLamp(index)" />
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

    const toggleLamp = (index: number) => {
      lamps.value[index].isOn = !lamps.value[index].isOn;
      const binaryString = lamps.value.map(lamp => (lamp.isOn ? '1' : '0')).join('');
      decimalNumber.value = parseInt(binaryString, 2);
    };

    updateLamps();

    return {
      decimalNumber,
      lamps,
      updateLamps,
      toggleLamp,
    };
  },
});
</script>
