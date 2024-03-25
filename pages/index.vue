<template>
  <main>
    <section ref="main" class="boxes-container">
      <h1>Use the button to toggle a Timeline</h1>
      <div>
        <button @click="toggleTimeline">Toggle Timeline</button>
      </div>
      <div class="box">Box 1</div>
      <div class="box">Box 2</div>
      <div class="box">Box 3</div>
    </section>
  </main>
</template>

<script>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

export default {
  name: 'IndexPage',
  mounted() {
    this.ctx = gsap.context((self) => {
      const boxes = self.selector('.box');
      this.tl = gsap
        .timeline()
        .to(boxes[0], { x: 120, rotation: 360 })
        .to(boxes[1], { x: -120, rotation: -360 }, '<')
        .to(boxes[2], { y: -166 })
        .reverse();
    }, this.$refs.main);
    ScrollTrigger.create({
      trigger: '.boxes-container',
    });
  },
  beforeDestroy() {
    this.ctx.revert();
  },
  methods: {
    toggleTimeline() {
      this.tl.reversed(!this.tl.reversed());
    },
  },
};
</script>
