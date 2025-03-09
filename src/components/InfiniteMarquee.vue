<template>
  <div class="marquee">
    <ul class="marquee-content">
      <li>
        <i class="fab fa-html5"></i>
        <p>html</p>
      </li>
      <li>
        <i class="fab fa-css3-alt"></i>
        <p>css</p>
      </li>
      <li>
        <i class="fab fa-js"></i>
        <p>js</p>
      </li>
      <li>
        <i class="fab fa-python"></i>
        <p>python</p>
      </li>
      <li>
        <i class="fab fa-docker"></i>
        <p>docker</p>
      </li>
      <li>
        <i class="fab fa-git"></i>
        <p>git</p>
      </li>
      <li>
        <i class="fab fa-linux"></i>
        <p>linux</p>
      </li>
    </ul>
    <ul class="marquee-content" aria-hidden="true">
      <li>
        <i class="fab fa-html5"></i>
        <p>html</p>
      </li>
      <li>
        <i class="fab fa-css3-alt"></i>
        <p>css</p>
      </li>
      <li>
        <i class="fab fa-js"></i>
        <p>js</p>
      </li>
      <li>
        <i class="fab fa-python"></i>
        <p>python</p>
      </li>
      <li>
        <i class="fab fa-docker"></i>
        <p>docker</p>
      </li>
      <li>
        <i class="fab fa-git"></i>
        <p>git</p>
      </li>
      <li>
        <i class="fab fa-linux"></i>
        <p>linux</p>
      </li>
    </ul>
  </div>
</template>

<script lang="js">
export default {
  name: 'InfiniteMarquee'
}
</script>

<style lang="scss" scoped>
$gap: 5rem;

.marquee {
  padding: 50px 0 50px 0;
  gap: $gap;
  display: flex;
  user-select: none;
  overflow: clip;
  width: 300px;
  mask-image: linear-gradient(
    to right,
    transparent,
    white 50%,
    transparent
  );

  .marquee-content {
    list-style-type: none;
    flex-shrink: 0;
    display: flex;
    justify-content: space-around;
    min-width: 100%;
    width: max-content;
    gap: $gap;
    animation: track 40s linear infinite;
    padding: 150px 0 150px 0;

    li {
      font-family: 'LeagueSpartan';
      font-size: 30px;
      color: #8ff;
      text-shadow: 0 0 20px rgba(0,255,255,0.95);

      height: 100px;
      width: 175px;

      position: relative;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 10px;

      border: 1px solid #8ff;
      border-radius: 5px;
      box-shadow: 5px 5px 0px #8ff;

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
      background-size: 2px 2px;
      pointer-events: none;
      i {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        top: -30px;
        right: 10px;
        width: 60px;
        height: 60px;
        border-radius: 50px;
      }
    }
  }
}

@keyframes track {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(calc(-100% - $gap))
  }
}

@media (min-width: 480px) {
  .marquee {
    width: 400px;
  }
}

@media (min-width: 768px) {
  .marquee {
    width: 500px;
  }
}

@media (min-width: 992px) {
  .marquee {
    width: 600px;
  }
}

@media (min-width: 1200px) {
  .marquee {
    width: 850px;
  }
}
</style>
