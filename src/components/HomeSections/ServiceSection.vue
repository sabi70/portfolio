<template>
  <div id="services">
    <div>
      <p>MY SERVICE</p>
      <p>Crafting seamless digital experiences from code to design.</p>
    </div>
    <div id="service-container">
      <ServiceBlock
        v-for="(title , index) in serviceTitle"
        :key="index"
        :serviceLogo="serviceLogo[index]"
        :serviceTitle="serviceTitle[index]"
        :serviceDescription="serviceDescription[index]"
        class="hidden"
      />
    </div>
  </div>
</template>

<script lang="js">
import ServiceBlock from '@/components/Service.vue';

export default {
  name: 'ServiceSection',
  components: {
    ServiceBlock
  },
  data() {
    return {
      serviceTitle: ['WEBSITE DEVELOPMENT', 'INTERFACE DESIGN', 'LOGO CREATION', 'SERVICE AUTOMATION'],
      serviceDescription: [
        'Creating Stunning Digital Experiences: From Ftontend and Backend Development to Creative Design. Your all-in-one solution for exceptional web projects. ',
        'Intuitive and Elegant Interface Design: Crafting user-centric, visually appealing, and functional design to enhance user experience and engagement.',
        'Crafing Unique and Memorable Logos: Designing visually striking and meaningful logos that reflect your brand\'s identity. Elevating your business image with professional logo creation servieces tailored to your needs.',
        'Streamlining Operations with Service Automation: Enhancing efficiency, reducing manual tasks, and optimizing workflows through innovative automation solutions tailored for your business needs.'
      ],
      serviceLogo: [
        'WD',
        'UI',
        'LC',
        'SA'
      ]
    }
  },
  mounted() {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        entry.target.classList.toggle('show', entry.isIntersecting);
      })
    }, {
      threshold: 0.6,
    })

    const elements = document.querySelectorAll('.hidden');
    elements.forEach(el => {
      observer.observe(el);
    });
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';
#services {
  display: flex;
  flex-direction: column;
  align-items: center;

  padding-top: 100px;

  height: auto;
  //background-color: rgba(255,255,255,0.1);
}
div {
  display: flex;
  flex-direction: column;
  align-items: center;
}
p:first-of-type {
  color: $neon-text;
  font-size: $font-size-base;
}

p:nth-of-type(2) {
  font-size: $font-size-header-2;
  width: 85%;
  margin-top: 15px;
  text-align: justify;
  font-weight: bold;
}

#service-container {
  margin-top: 50px;
  width: auto;
  display: flex;
  flex-direction: column;
  gap: 75px;
}


// intersection observer

.hidden {
  opacity: 0;
  transform: translateX(-15%);
  transition: 150ms ease-out;
}

.hidden.show {
  opacity: 1;
  transform: translateX(0);
}

@media (min-width: 992px) {
  #service-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 50px;
  }
}
</style>