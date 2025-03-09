<template>
  <nav id="header">
    <router-link to="/">
      <img :src="lego">
    </router-link>
    <ul>
      <li>
        <router-link to="/projects">Projects</router-link>
      </li>
      <li>
        <router-link to="/about">About</router-link>
      </li>
    </ul>
  </nav>
</template>
<script lang="js">
import logo from '@/assets/images/logo/logo.png'

export default {
  name: 'HeaderComponent',
  data() {
    return {
      lego: logo
    };
  }
};
</script>
<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';

#header {
  width: 85%;
  height: 40px;
  
  font-family: 'LeagueSpartan';

  border-radius: 5px;
  border-width: 0.5px;
  border-style: double;
  border-color: $neon-border;
  background-color: $neon-surface;
  backdrop-filter: blur(10px);
  box-shadow: 0px 0px 12px $neon-shadow;

  margin: auto;
  margin-top: 20px;
  margin-bottom: 5px;
  padding: 12px 20px 10px 15px;

  display: flex;
  justify-content: space-between;
  align-items: center;
}
#header img {
  width: 35px;
  height: 35px;
}
#header ul {
  list-style-type: none;
  display: flex;
  gap: 15px;
}
#header ul li a {
  font-size: 15px;
  color: $neon-text;
  text-decoration: none;
}
#header ul li .router-link-active {
  transition: 1s;
  text-decoration: underline;
  text-shadow: 0px 0px 15px $neon-text-shadow;
}

#myLogo {
  position: absolute;
  left: 18px;
}

// MEDIA QUERIES FOR RESPONSIVNESS. BREAKPOINTS: 480, 768, 992, 1200;
@media screen and (min-width: 480px) {
  #header {
    width: 75%;
  }
}

@media screen and (min-width: 768px) {
  #header {
    width: 65%;
  }
}

@media screen and (min-width: 992px) {
  #header {
    width: 60%;
  }
}
</style>