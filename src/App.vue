<template>
  <div class="calculator">
    <input
        type="text"
        v-model="display"
        class="display"
        disabled
    >

    <div class="buttons">
      <button
          v-for="btn in buttons"
          :key="btn.value"
          @click="update(btn.value)"
          :class="`button button_${btn.type || 'default'}`"
      >
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    // data
    const display = ref('');
    const buttons = [
      {value: 'AC', type: 'clear'},
      {value: 'DEL', type: 'delete'},
      {value: '.', type: 'operator'},
      {value: '/', type: 'operator'},

      {value: '7'},
      {value: '8'},
      {value: '9'},
      {value: '*', type: 'operator'},

      {value: '4'},
      {value: '5'},
      {value: '6'},
      {value: '-', type: 'operator'},

      {value: '1'},
      {value: '2'},
      {value: '3'},
      {value: '+', type: 'operator'},

      {value: '000'},
      {value: '00'},
      {value: '0'},
      {value: '=', type: 'equals'},
    ]

    // methods
    const update = (value) => {
      if (value === 'AC') {
        return display.value = '';
      }

      if (value === 'DEL') {
        return display.value = display.value.slice(0, -1);
      }

      if (value === '=') {
        return display.value = eval(display.value);
      }

      display.value += value;
    };

    return {
      display,
      buttons,
      update
    }
  }
}
</script>