<template>
  <div class="popup" :class="{ open: isOpen, closed: !isOpen }">
    {{ text }}
  </div>
</template>

<script>
export default {
  name: "Popup",
  data() {
    return {
      isOpen: false,
      text: ""
    }
  },
  methods: {
    showPopup(text) {

      // Don't do anything if popup is open
      if(this.isOpen) return;

      this.text = text;
      this.isOpen = true;

      // Close after three secodns
      setTimeout(() => {
        this.isOpen = false;
      }, 5000);
    }
  }
}
</script>

<style scoped>

.popup {
  position: fixed;
  background: red;
  height: 150px;
  width: 400px;

  right: 0;
  bottom: 0;

  transition: transform 0.5s ease;
}

.open {
  transform: translateY(0);
}

.closed {
  transform: translateY(150px);
}
</style>