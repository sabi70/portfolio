<template>
  <div id="project-container">
    <img :src="image">
    <div id="project-info">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <div id="skills">
      <i 
        v-for="(icon, index) in icons"
        :key="index"
        :class="icon"
      >
      </i>
    </div>
    <div id="github-link-btn">
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
export default {
  name: 'ProjectComponent',
  data() {
    return {};
  },
  props: {
    image: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    githubLink: {
      type: String,
      required: true
    },
    icons: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';

img {
  max-width: 300px;
}

#project-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 25px;

  width: 300px;
  height: 560px;
  padding-bottom: 25px;

  border: 1px solid rgba(0,127,127, 1);
  border-radius: 5px;

  background-image:
    linear-gradient(
      90deg,
      rgba(0,127,127, 0.2),
      transparent 1px
    ),
    linear-gradient(
      rgba(0,127,127, 0.2),
      transparent 1px
    );
  background-size: 3.5px 3.5px;

  #project-info {
    display: flex;
    flex-direction: column;
    gap: 5px;
    width: 85%;
    text-align: justify;
  }

  #github-link-btn {
    position: absolute;
    bottom: 25px;
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
    i {
      font-size: 20px;
      padding-inline: 5px;
    }
    a {
      text-decoration: none;
    }
  }

  #skills {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 10px;

    i {
      font-size: 30px;
      
    }

    .fa-html5 {
      color: #e34f26;
    }
    .fa-css3-alt {
      color: #1572b6;
    }
    .fa-sass {
      color: #cd6799;
    }
    .fa-js {
      color: #f7df1e;
    }
    .fa-vuejs {
      color: #41b883;
    }
    .fa-figma {
      color: #1abcfe;
    }
    .fa-python {
      color: #3776ab;
    }
    .fa-docker {
      color: #2496ed;
    }
  }
}
</style>
