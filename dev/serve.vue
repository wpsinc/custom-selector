<script>
import { defineComponent } from 'vue';
import CustomSelector from '@/custom-selector.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    CustomSelector
  }
});
</script>

<template>
  <div id="app">
    <custom-selector />
  </div>
</template>
