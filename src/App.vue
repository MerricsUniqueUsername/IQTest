<template>

  <Quiz />

  <!-- Popup -->
  <Popup ref="popup"/>


</template>

<script>
import Quiz from "./components/Quiz.vue"
import Popup from "./components/Popup.vue"

export default {
  name: 'App',
  components: {
    Quiz,
    Popup,
  },
  methods: {
    showPopup(text) {
      this.$refs.popup.showPopup(text);
    },
  }

}
</script>

<style>

</style>