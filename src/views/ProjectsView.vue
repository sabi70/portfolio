<template>
  <div class="projects">
    <div id="projects-container">
      <ProjectComponent
        v-for="(image, index) in images"
        :key="index"
        :image="image"
        :title="titles[index]"
        :description="descriptions[index]"
        :githubLink="githubLinks[index]"
        :icons="icons[index]"
        class="hidden"
      />
    </div>
  </div>
</template>
<script lang="js">
import ProjectComponent from '@/components/Project.vue';

import portfolio from '@/assets/images/projects/portfolio.webp';
import todobuddy from '@/assets/images/projects/todobuddy.webp';
import localChatroom from '@/assets/images/projects/local-chatroom.webp';
import usaStates from '@/assets/images/projects/usa-states-game.webp';

export default {
  components: {
    ProjectComponent
  },
  data() {
    return {
      images: [
        portfolio,
        todobuddy,
        localChatroom,
        usaStates
      ],
      titles: [
        'Portfolio Website',
        'TodoBuddy',
        'Local Chatroom',
        'US States Game'
      ],
      descriptions: [
        'My portfolio website showcases my wor, skills, and achievements, giving visitors a clear picture of what i bring to table.',
        'TodoBuddy is your personal task management companion, designed to help you organize, prioritize, and track your to-do list effortlessly.',
        'A local chatroom on a local network using sockets allows users to communicate in real-time without requiring an internet connection.',
        'The US States Guessing Game challenges players to name all 50 states, testing their geographical knowledge.'
      ],
      githubLinks: [
        'https://github.com/sabi70/portfolio/',
        'https://github.com/sabi70/todobuddy/',
        'https://github.com/sabi70/LocalChatroom/',
        'https://github.com/sabi70/us-states-game/',
      ],
      icons: [
        ['fab fa-html5', 'fab fa-sass', 'fab fa-js', 'fab fa-vuejs', 'fab fa-figma'],
        ['fab fa-html5', 'fab fa-css3-alt', 'fab fa-js', 'fab fa-vuejs', 'fab fa-python', 'fab fa-docker'],
        ['fab fa-python'],
        ['fab fa-python'],
      ]
    };
  },
  mounted() {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        entry.target.classList.toggle('show', entry.isIntersecting);
      })
    }, {
      threshold: 0.3,
    })

    const elements = document.querySelectorAll('.hidden');
    elements.forEach(el => {
      observer.observe(el);
    });
  }
}

</script>
<style lang="scss" scoped>
.projects {
  display: flex;
  justify-content: center;

  width: 100%;
  height: 100%;
  margin-bottom: 150px;
}

#projects-container {
  display: flex;
  flex-wrap: wrap;  
  justify-content: center;    

  height: 100%;
  width: 75%;
  row-gap: 0px;
  column-gap: 75px;
}

.hidden {
  opacity: 0;
  transform: translateX(-15%);
  transition: 350ms ease-out;
}

.hidden.show {
  opacity: 1;
  transform: translateX(0);
}
</style>