<template>
  <div ref="item">
    <p style="display: flex; align-items: center; justify-content: center;">Calculating IQ...</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "EndScreen",
  props: ['answers'],
  data() {
    return {
      res: '',
    }
  },
  methods: {
    calculateIq() {
      axios.post('https://iqtestbackend.vercel.app/estimate_iq/', {
          currentAnswers: this.answers
      })
      .then(response => {
          this.res = response.data.replace('html', '').replace('```', '');

          // Change innerHTML of item ref
          this.$refs.item.innerHTML = `${this.res}`;
      })
      .catch(error => {
          console.error(error);
          
          // Try again
          this.calculateIq();
      });
    }
  }
}
</script>

<style>

</style>