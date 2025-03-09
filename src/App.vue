<template>
  <!--<router-link to="/about">About</router-link>-->
  <PreLoad :preloadState="preloadState" />
  <ScrollFAB />
  <div id="gridContainer">
    <nav><HeaderComponent /></nav>
    <main>
      <router-view/>
    </main>
    <footer>
      <FooterComponent />
    </footer>
  </div>
</template>
<script lang="js">
import HeaderComponent from '@/components/Header.vue';
import FooterComponent from '@/components/Footer.vue';
import ScrollFAB from '@/components/ScrollFAB.vue';
import PreLoad from '@/components/PreLoad.vue';

export default {
  components: {
    HeaderComponent,
    FooterComponent,
    ScrollFAB,
    PreLoad
  },
  data() {
    return {
      preloadState: true,
    }
  },
  mounted() {
    window.onload = () => {
      setTimeout(() => { this.preloadState = false });
    };
  }
};
</script>
<style lang="scss">
@font-face {
  font-family: 'LeagueSpartan';
  src: url('@/assets/fonts/RoboticModern.ttf') format(opentype);
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: 'VarelaRound';
  src: url('@/assets/fonts/VarelaRound.ttf') format(opentype);
  font-weight: normal;
  font-style: normal;
}

#app {
  font-family: 'VarelaRound';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f8f8ff;
}

img {
  user-select: none;
  pointer-events: none;
}

// GRIDS
// HEADER
nav {
  position: sticky;
  top: 0;
  grid-area: header;
  z-index: 1000;
}
// MAIN
main {
  grid-area: main;
  background-color: transparent;
}
// FOOTER
footer {
  grid-area: footer;
}
// GRID CONTAINER 
#gridContainer {
  display: grid;
  gap: 10px;
  height: 100%;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    'header'
    'main'
    'footer'
  ;
}
</style>
