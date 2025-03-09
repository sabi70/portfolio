<template>
  <div id="service-card">
    <div id="service-content">
      <div id="service-logo">{{ serviceLogo }}</div>
      <p>{{ serviceTitle }}</p>
      <p>{{ serviceDescription }}</p>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'ServiceBlock',
  props: {
    serviceLogo: {
      type: String,
      required: true
    },
    serviceTitle: {
      type: String,
      required: true
    },
    serviceDescription: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';

#service-card {
  width: 300px;
  height: 375px;

  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  
  font-family: 'VarelaRound';
  
  background: $github-dark;
  border-radius: $border-radius-base;
  transition: 0.5s;
  box-shadow: 0px 0px 3px 1px rgba(0,255,255,0.2);
  cursor: pointer;
  overflow: hidden;

  #service-content {
    width: calc(100% - 5px);
    height: calc(100% - 5px);

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    gap: 20px;

    border-radius: $border-radius-base;
    background: $github-dark;
    
    background-image:
      linear-gradient(
        90deg,
        rgba(0,127,127, 0.5),
        transparent 1px
      ),
      linear-gradient(
        rgba(0,127,127, 0.5),
        transparent 1px
      );
    background-size: 1px 1px;
    pointer-events: none;

    z-index: 1;

    p:first-of-type {
      font-size: 18px;
    }

    p:nth-of-type(2) {
      font-size: 18px;
      text-align: justify;
      width: 85%;

      color: rgba(255,255,255,0.6);
    }

    #service-logo {
      width: 75px;
      height: 75px;

      display: flex;
      justify-content: center;
      align-items: center;

      font-size: 45px;
      font-family: 'LeagueSpartan';
      color: $neon-text;
      text-shadow: 0 0 5px $neon-text-shadow;

      background-color: $neon-surface;
      box-shadow: 0 0 20px $neon-shadow;
      border: 1px solid $neon-border;
      border-radius: $border-radius-base;
    }
  }
}

#service-card::before {
  opacity: 0;
  content: ' ';
  position: absolute;
  display: block;
  width: 120px;
  height: 300px;
  transform: rotate(0deg) translateY(50%);
  background: linear-gradient(90deg, $neon-border, transparent);
  transition: opacity 300ms;
  animation: border-rotation-neon 3000ms infinite linear;
  animation-play-state: paused;
}

#service-card::after {
  opacity: 0;
  content: ' ';
  position: absolute;
  display: block;
  width: 120px;
  height: 300px;
  transform: rotate(0deg) translateY(-50%);
  background: linear-gradient(90deg, $sakura-border, transparent);
  transition: opacity 300ms;
  animation: border-rotation-sakura 3000ms infinite linear;
  animation-play-state: paused;
}

#service-card:hover {
  box-shadow: none;
}

#service-card:hover::before {
  opacity: 1;
  animation-play-state: running;
}

#service-card:hover::after {
  opacity: 1;
  animation-play-state: running;
}


@keyframes border-rotation-neon {
  0% {
    transform: rotate(0deg) translateY(50%);
  }
  100% {
    transform: rotate(360deg) translateY(50%);
  }
}

@keyframes border-rotation-sakura {
  0% {
    transform: rotate(0deg) translateY(-50%);
  }
  100% {
    transform: rotate(360deg) translateY(-50%);
  }
}

@media (min-width: 480px) {
  #service-card {
    width: 400px;
  }
}

@media (min-width: 768px) {
  #service-card {
    width: 600px;
    height: 300px;
  }

  #service-card::before {
    height: 330px;
  }

  #service-card::after {
    height: 330px;
  }
}

@media (min-width: 992px) {
  #service-card {
    width: 35%;
    height: 350px;
  }
}

@media (min-width: 1200px) {
  #service-card {
    width: 35%;
    height: 350px;
  }
}

</style>
