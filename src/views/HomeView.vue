<template>
  <section>
    <IntroSection />
  </section>
  <section>
    <ServiceSection />
  </section>
  <section style="display: flex; align-items:center; justify-content: center;">
    <InfiniteMarquee />
  </section>
</template>

<script>
// SECTIONS
import IntroSection from '@/components/HomeSections/IntroSection.vue'
import ServiceSection from '@/components/HomeSections/ServiceSection.vue'
import InfiniteMarquee from '@/components/InfiniteMarquee.vue';

export default {
  name: 'HomeView',
  components: {
    IntroSection,
    ServiceSection,
    InfiniteMarquee
  },
  data() {
    return {};
  },  
}
</script>
<style lang="scss" scoped></style>