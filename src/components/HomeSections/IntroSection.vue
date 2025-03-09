<template>
  <div id="intro">
    <div style="display: flex; gap: 25px;">
      <p id="label-text">Hi<span>,</span> I'm</p>
      <LabelComponent :contentText="labelBoxContent" />
    </div>
    <p id="label-greeting">
      <span>Welcome</span> to my 
      <span>digital</span>
        corner!
    </p>
    <div class="contact-buttons">
      <a :href="instagramLink">
        <div>
          <i class="fab fa-instagram"></i>
          Instagram
        </div>
      </a>
      <a :href="githubLink">
        <div>
          <i class="fab fa-github"></i>
          Github
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import LabelComponent from '@/components/Label.vue';

export default {
  name: 'IntroSection',
  components: {
    LabelComponent
  },
  data() {
    return {
      instagramLink: 'https://www.instagram.com/s274abi/',
      githubLink: 'https://github.com/sabi70',
      labelBoxContent: [
        'WEB DEVELOPER',
        'ENTHUSIAST',
        'PLAYER',
        'CODER'
      ]
    };
  }
}
</script>

<style lang='scss' scoped>
@import '@/assets/styles/_variables.scss';

#intro {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height:500px;

  font-family: 'LeagueSpartan';

  #label-text {
    font-size: 46px;
  }

  #label-text span {
    color: $neon-text;
  }

  #label-greeting {
    padding-top: 25px;
    font-size: 17px;

    span:first-of-type {
      color: $sakura-text;
      font-style: italic;
    }
    span:nth-of-type(2) {
      color: $neon-text;
      text-decoration:line-through;
    }
  }

  .contact-buttons {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 25px;

    div {
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;

      width: 250px;
      padding: 10px 8px 10px 8px;
      border-radius: $border-radius-small;
      font-size: $font-size-base;
    }
    a:first-of-type div {
      background: $sakura-text;
      color: $github-dark;
    }
    a:nth-of-type(2) div {
      background: $github-dark;
      color: $sakura-text;
      border: 1px solid $sakura-text;
    }
    i {
      font-size: 20px;
      padding-inline: 5px;
    }
    a {
      text-decoration: none;
    }
  }
}
</style>
