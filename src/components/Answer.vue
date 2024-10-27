<template>
  <div>
    <button class="button">{{ text }}</button>
  </div>
</template>

<script>
export default {
  name:'Answer',
  props: ['text'],
}
</script>

<style scoped>
.button {
  /* Core sizing */
  padding: 14px 32px;
  width: 350px;
  height: 120px;

  /* Premium typography */
  font-family: 'Trebuchet MS', sans-serif;
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 0.5px;
  line-height: 1.4;
  text-transform: uppercase;

  /* Sophisticated grayscale palette */
  /* background: linear-gradient(180deg, #424242 0%, #383838 100%);
  color: #FFFFFF;
  border: 1px solid #2A2A2A;
  border-bottom: 2px solid #1A1A1A;
  border-radius: 6px; */

  /* Professional effects */
  box-shadow: 
  0 2px 4px rgba(0, 0, 0, 0.1),
  0 4px 8px rgba(0, 0, 0, 0.05),
  inset 0 1px 0 rgba(255, 255, 255, 0.1);

  /* Refined transitions */
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);

  /* Polished defaults */
  cursor: pointer;
  outline: none;
  position: relative;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Hover interaction */
.button:hover {
  /* background: linear-gradient(180deg, #4A4A4A 0%, #404040 100%); */
  box-shadow: 
  0 4px 8px rgba(0, 0, 0, 0.15),
  0 8px 16px rgba(0, 0, 0, 0.1),
  inset 0 1px 0 rgba(255, 255, 255, 0.15);
  transform: translateY(-1px);
}

/* Active state */
.button:active {
  /* background: linear-gradient(180deg, #363636 0%, #3A3A3A 100%); */
  box-shadow: 
  0 1px 2px rgba(0, 0, 0, 0.2),
  inset 0 1px 2px rgba(0, 0, 0, 0.15);
  transform: translateY(1px);
  outline: none;
}

/* Focus state */
.button:focus {
  box-shadow: 
  0 0 0 3px rgba(42, 42, 42, 0.4),
  0 2px 4px rgba(0, 0, 0, 0.1);
  outline: none;
}

/* Disabled state */
.button:disabled {
  background: linear-gradient(180deg, #9E9E9E 0%, #888888 100%);
  border-color: #7A7A7A;
  color: rgba(255, 255, 255, 0.7);
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

/* Optional: Add subtle text shadow for depth */
.button {
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
}

/* Optional: Add a very subtle inner glow */
.button::before {
  content: '';
  position: absolute;
  top: 1px;
  left: 1px;
  right: 1px;
  height: 1px;
  background: linear-gradient(90deg, 
    rgba(255, 255, 255, 0.1), 
    rgba(255, 255, 255, 0.15), 
    rgba(255, 255, 255, 0.1)
  );
  border-radius: 6px 6px 0 0;
}
</style>
