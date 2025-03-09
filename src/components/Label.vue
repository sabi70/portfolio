<template>
  <div id="label-container">
    <div class="perspective">
      <div class="box">
        <div class="side top">{{ contentText[0] }}</div>
        <div class="side bottom">{{ contentText[1] }}</div>
        <div class="side back">{{ contentText[2] }}</div>
        <div class="side front">{{ contentText[3] }}</div>
      </div>
    </div>    
  </div>
</template>
<script lang="js">
export default {
  name: 'LabelComponent',
  props: {
    contentText: {
      type: Array,
      required: true
    }
  }
}
</script>
<style lang="scss" scoped>
@import '@/assets/styles/label_box.scss';
$box-width: 110px;

#label-container {
  display: flex;
  justify-content: center;
  gap: 20px;
}
.perspective {
  position: relative;
  display: inline-block;
  perspective: 1000px;
  perspective-origin: 250% -200%;
  width: 100px;  
}
.box {
  width: $box-width;
  position: relative;

  aspect-ratio: 2;

  transform-style: preserve-3d;
  transform-origin: 0px center 0px;
  animation: rotate 10s ease-in-out infinite;
}
  .side {
    @include box-theme;
    position: absolute;

    width: $box-width;
    border-radius: 2px;
    border-width: 3px;
    border-style: double;
    
    backdrop-filter: blur(1.5px);

    font-size: 16px;
    font-weight: bold;

    display: flex;
    flex-direction: column;
    justify-content: center;

    aspect-ratio: 2;
    transform-style: preserve-3d;
  }

  .side.top {
    transform: rotateX(90deg) translateZ(30px);
  }
  .side.bottom {        
    transform: rotateX(-90deg) translateZ(30px);
  }
  .side.back {    
    transform: rotateX(180deg) translateZ(30px);
  }
  .side.front {
    transform: rotateX(0deg) translateZ(30px);
  }

  @keyframes rotate {
    0% {
      transform: rotateX(0deg);
    }
    25% {
      transform: rotateX(90deg);
    }
    50% {
      transform: rotateX(180deg);
    }
    75% {
      transform: rotateX(270deg);
    }
    100% {
      transform: rotateX(360deg);
    }
  }
</style>