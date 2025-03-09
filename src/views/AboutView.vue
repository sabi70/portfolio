<template>
  <div class="about">
    <!-- <ThreeModel :customStyle="customStyle"/> -->
    <div id="about-container">
      <div id="player-img-container">
        <img :src="player" id="player-img">
      </div>
      <div id="player-info">
        <div>
          <h3>Education</h3>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, reprehenderit quos iusto dolor iste odio consectetur placeat accusantium hic? Totam ipsam at exercitationem ullam nesciunt recusandae? Tempora itaque, natus quasi iusto harum impedit sunt doloremque dolore reiciendis beatae reprehenderit labore ipsa velit ducimus dolorem vel asperiores ipsam veniam incidunt pariatur, consequatur nihil neque. Ab, a!</p>
        </div>
        <div>
          <h3>Career</h3>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, reprehenderit quos iusto dolor iste odio consectetur placeat accusantium hic? Totam ipsam at exercitationem ullam nesciunt recusandae? Tempora itaque, natus quasi iusto harum impedit sunt doloremque dolore reiciendis beatae reprehenderit labore ipsa velit ducimus dolorem vel asperiores ipsam veniam incidunt pariatur, consequatur nihil neque. Ab, a!</p>
        </div>
        <div>
          <h3>Projects</h3>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, reprehenderit quos iusto dolor iste odio consectetur placeat accusantium hic? Totam ipsam at exercitationem ullam nesciunt recusandae? Tempora itaque, natus quasi iusto harum impedit sunt doloremque dolore reiciendis beatae reprehenderit labore ipsa velit ducimus dolorem vel asperiores ipsam veniam incidunt pariatur, consequatur nihil neque. Ab, a!</p>
        </div>
      </div>
      <div id="skill-box">
        <ThreeModel :customStyle="customStyle" v-if="webGLSupport"/>
        <div v-else id="caution">
          <h2>Your browser doesnt support WebGL!</h2>
        </div>
      </div>
      <div id="contacts-container">
        <h2>Contacts:</h2>
        <div class="hidden">
          <i class="fa-solid fa-phone"></i>
          <h3>Lets talk us</h3>
          <p>+8 61-10-78-99</p>
        </div>
        <div class="hidden">
          <i class="fa-solid fa-envelope-open-text"></i>
          <h3>Send us email</h3>
          <a href="mailto:s274abi@gmail.com">s274abi@gmail.com</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="js">
import WebGL from 'three/addons/capabilities/WebGL.js';
import ThreeModel from '@/components/ThreeModel.vue';
import player from '@/assets/images/player/player_4.jpeg'

export default {
  name: 'AboutView',
  components: {
    ThreeModel
  },
  data() {
    return {
      customStyle: {
        width: 'auto',
        height: '400px'
      },
      player: player,
      webglSupport: false,
    }
  },
  beforeMount() {
    this.checkWebGLSupport();
  },
  mounted() {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        entry.target.classList.toggle('show', entry.isIntersecting);
      })
    }, {
      threshold: 0.8,
    })

    const elements = document.querySelectorAll('.hidden');
    elements.forEach(el => {
      observer.observe(el);
    });
  },
  methods: {
    checkWebGLSupport() {
      if (WebGL.isWebGL2Available()) {
        this.webGLSupport = true;
      } else {
        this.webGLSupport = false;
      }
    }
  }  
}
</script>
<style lang="scss" scoped>
.about {
  display: flex;
  flex-direction: column;
  text-align: justify;
  font-size: 18px;
  padding-bottom: 75px;
  height: 100%;
}
#about-container {
  margin-bottom: 50px;
  width: 100%;
  height: auto;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 50px;

  #player-img-container {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    background-image:
      linear-gradient(
        90deg,
        rgba(0,127,127, 0.6),
        transparent 1px
      ),
      linear-gradient(
        rgba(0,127,127, 0.6),
        transparent 1px
      );
    background-size: 5px 5px;
    pointer-events: none;
  }
  
  #player-img {
    width: 100%;
    max-width: 550px;
  }

  #skill-box {
    width: 100%;
    height: auto;

    display: flex;
    justify-content: center;
    align-items: center;

    #caution {
      padding: 25px;
      width: 60%;
      text-align: center;
      background: rgba(0,127,127,0.2);
      border-radius: 10px;
      border: 2px solid rgba(0,127,127,1);
      box-shadow: 0 0 10px rgba(0,127,127,1);

      color: rgba(255,255,255,0.75);
      text-shadow: 0 0 10px rgba(0,255,255,0.95);
    }
  }

  #contacts-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 40px;
    
    div {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      gap: 8px;

      a {
        color: white;
        text-decoration: none;
      }
    }
    
    i {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100px;
      height: 100px;
      border-radius: 50px;
      font-size: 50px;
      color: rgba(255,255,255,0.75);
      text-shadow: 0 0 10px rgba(0,255,255,0.95);
      background: rgba(0,127,127,0.5);
      
    }
  }

}

// intersection observer
.hidden {
  opacity: 0;
  transform: translateX(-15%);
  transition: 350ms ease-out;
}

.hidden.show {
  opacity: 1;
  transform: translateX(0);
}

@media (max-width: 991px) {
  #player-info {
    width: 80%;
    display: flex;
    flex-direction: column;
    gap: 25px;

    div {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }
  }
}
@media (min-width: 992px) {
  #player-info {
    width: 90%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 50px;

    div {
      width: calc(90% / 3);
      display: flex;
      flex-direction: column;
      gap: 15px;
    }
  }
}
</style>
