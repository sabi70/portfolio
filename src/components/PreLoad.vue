<template>
  <div id="loader-container" :class="{ active: preloadState, inactive: !preloadState }">
    <div class="loader">
      <div class="orb" style="--index: 0"></div>
      <div class="orb" style="--index: 1"></div>
      <div class="orb" style="--index: 2"></div>
      <div class="orb" style="--index: 3"></div>
      <div class="orb" style="--index: 4"></div>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'PreLoad',
  props: {
    preloadState: {
      type: Boolean
    }
  }
}
</script>

<style lang="scss" scoped>
$size-loader: 40px;
$size-orb: 10px;

.inactive {
  transform: translateY(-100%);
  opacity: 0;
  transition: 2s;
}
#loader-container {
  position: fixed;
  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  background-color: #0d1117;
  z-index: 9999;
  overflow: hidden;

  display: flex;
  justify-content: center;
  align-items: center;

  .loader {
    width: $size-loader;
    height: $size-loader;
    position: relative;
    transform: rotate(45deg);
  }

  .orb {
    position: absolute;
    width: 100%;
    height: 100%;
    --delay: calc(var(--index) * 0.05s);
    animation: orbit-rotate ease-in-out 1.5s var(--delay) infinite;
    opacity: calc(1 - calc(0.2 * var(--index)));
  }

  .orb::before {
    position: absolute;
    content: '';
    bottom: 0;
    right: 0;
    width: $size-orb;
    height: $size-orb;
    background-color: rgba(227,61,148,0.9);
    border-radius: 10px;
    box-shadow: 0px 0px 15px 10px rgba(227,61,148,0.2);
  }

  .orb::after {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    width: $size-orb;
    height: $size-orb;
    background-color: #8ff;
    border-radius: 10px;
    box-shadow: 0px 0px 30px 10px rgba(0,127,127,1);
  }
}

@keyframes orbit-rotate {
  0% {

  }
  50% {
    transform: rotate(360deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>