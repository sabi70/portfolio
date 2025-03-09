<template>
  <div id="fab">
    <i class="fas fa-angle-up"></i>
  </div>
</template>
<script lang="js">
export default {
  name: 'ScrollFAB',
  mounted() {
    window.addEventListener('scroll', function() {
      const fab = document.getElementById('fab');
      const scrollTop = this.window.scrollY || document.documentElement.scrollTop;
      const scrollHeight = 
        this.document.documentElement.scrollHeight - document.documentElement.clientHeight;
      const scrollPercentage = (scrollTop / scrollHeight) * 100;
      const degrees = (scrollPercentage / 100) * 360;
      
      fab.style.background = `conic-gradient(rgba(0,255,255,0.5) ${degrees}deg, transparent ${degrees}deg)`;
    });
    document.getElementById('fab').addEventListener('click', function() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    });
  },

}
</script>

<style lang="scss" scoped>
#fab {
  width: 50px;
  height: 50px;

  position: fixed;
  display: flex;
  z-index: 2;
  justify-content: center;
  align-items: center;

  bottom: 50px;
  right: 50px;

  border-radius: 25px;

  i {
    width: calc(100% - 3px);
    height: calc(100% - 3px);

    background: #0d1117;
    box-shadow: 0 0 15px rgba(0,255,255,0.5);
    color: rgba(0,255,255,0.5);
    font-size: 20px;

    border-radius: 25px;

    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>