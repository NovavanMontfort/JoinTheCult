<template>
  <div class="container">
    <div id="kinetic-type" ref="kineticType">
      <!-- maakt 20 lijnen -->
      <div
        v-for="n in 20"
        :key="n"
        :class="n % 2 === 1 ? 'type-line odd' : 'type-line even'"
      >
        CULT JOIN THE CULT JOIN THE CULT JOIN THE CULT JOIN THE CULT JOIN THE CULT
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";
import { CustomEase } from "gsap/CustomEase";

gsap.registerPlugin(CustomEase);

const kineticType = ref(null);

onMounted(() => {
  CustomEase.create("customEase", "0.86, 0, 0.07, 1");

  const kineticEl = kineticType.value;
  const oddLines = kineticEl.querySelectorAll(".odd");
  const evenLines = kineticEl.querySelectorAll(".even");
  const TYPE_LINE_OPACITY = 0.99;

  gsap.set(oddLines, { opacity: TYPE_LINE_OPACITY });
  gsap.set(evenLines, { opacity: TYPE_LINE_OPACITY });

  const timeline = gsap.timeline({ repeat: -1, defaults: { ease: "customEase" } });
  timeline.to(kineticEl, { duration: 1.4, scale: 2.3, rotation: -90 })
    .to(oddLines, { x: "20%", duration: 1, stagger: 0.08 }, "<")
    .to(evenLines, { x: "-20%", duration: 1, stagger: 0.08 }, "<")
    .to(oddLines, { x: "-200%", duration: 1.5, stagger: 0.08 }, ">")
    .to(evenLines, { x: "200%", duration: 1.5, stagger: 0.08 }, "<")
    .to(kineticEl, { opacity: 0, duration: 1.5 })
    .set(kineticEl, { rotation: 0, scale: 1, x: 0, opacity: 1 });
});
</script>

<style scoped>
.container {
  position: fixed;
  inset: 0;
  background: #000;
  color: white;
  font-family: "Inter Tight", sans-serif;
  user-select: none;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

#kinetic-type {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
  z-index: 10;

  transform-origin: center center;
  will-change: transform, opacity;
  backface-visibility: hidden;
  -webkit-font-smoothing: antialiased;
}

.type-line {
  display: block;
  width: max-content;
  white-space: nowrap;
  margin: 0;
  padding: 0;
  line-height: 0.8; /* strakker dan 1 */
  font-weight: 800;
  color: #fff;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  letter-spacing: 0.06em;
  will-change: transform, opacity;
  opacity: 1 !important;
}



.type-line.odd {
  color: #fff;
}

.type-line.even {
  color: #f2f2f2;
}

#kinetic-type > .type-line {
  padding-top: 0;
  padding-bottom: 0;
  margin: 0;
}

#kinetic-type::before,
#kinetic-type::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  height: 8vh;
  pointer-events: none;
  z-index: 20;
}
#kinetic-type::before {
  top: 0;
  background: linear-gradient(to bottom, #000 0%, transparent 100%);
}
#kinetic-type::after {
  bottom: 0;
  background: linear-gradient(to top, #000 0%, transparent 100%);
}

/* Responsive font sizes */
@media (min-width: 1400px) {
  #kinetic-type {
    font-size: clamp(3rem, 8vw, 12rem);
  }
}
@media (max-width: 1399px) {
  #kinetic-type {
    font-size: clamp(2.5rem, 9vw, 10.5rem);
  }
}
@media (max-width: 768px) {
  #kinetic-type {
    font-size: clamp(1.6rem, 8.5vw, 6rem);
  }
  #kinetic-type > .type-line {
    line-height: 0.85;
  }
}
</style>







