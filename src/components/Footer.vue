<template>
  <div class="footer">
    <h1>meylis</h1>
    <h3>My address in the digital world</h3>
    <div class="social-container">
      <a
        v-for="(link, index) in socialNetworkLinks"
        :key="index"
        :href="link"
      >
        <i :class="socialNetworkIcons[index]"></i>
      </a>
    </div>
  </div>
</template>

<script lang="js">

export default {
  name: 'FooterComponent',
  data() {
    return {
      socialNetworkLinks: [
        'https://www.instagram.com/s274abi',
        'https://t.me/sabi_to',
        'https://x.com/_sabico',
        'https://vk.com/id855742873'
      ],
      socialNetworkIcons: [
        'fab fa-instagram',
        'fab fa-telegram',
        'fab fa-x-twitter',
        'fab fa-vk'
      ]
    }
  }
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';

.footer {
  padding: 100px 0 100px 0;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 25px;
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

  h1 {
    pointer-events: none;
    position: absolute;
    top: -17.8px;
    font-family: 'LeagueSpartan';
    font-size: 50px;
    color: transparent;
    letter-spacing: 12px;
    background: linear-gradient(to bottom, rgba(0,127,127, 0.5) 50%, #0d1117 50%);
    background-clip: text;
  }

  .social-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: left;
    padding-left: 20px;
    gap: 25px;

    i {
      font-size: 25px;
      color: #fbfbfb;
    }
  }
}
</style>