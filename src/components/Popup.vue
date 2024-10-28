<template>
  <div class="popup" :class="{ open: isOpen, closed: !isOpen }">
    <h4>Notification: </h4>
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

* {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  color: rgb(21, 52, 82);
}

.popup {
  position: fixed;
  border: 1px, solid;
  border-color: rgb(60, 180, 200);
  background-color: rgb(226, 241, 255);
  height: 150px;
  width: 400px;
  border-radius: 3px;

  padding: 8px;
  padding-left: 14px;
  padding-right: 14px;

  right: 0;
  bottom: 0;

  /* Box shadow */
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1);

  transition: transform 0.5s ease;
}

.open {
  transform: translateY(0);
}

.closed {
  transform: translateY(180px);
}
</style>