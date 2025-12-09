<template>
  <div class="container">
    <div id="kinetic-type" ref="kineticType">
      <!-- Maak 15 lijnen, met afwisselend class odd/even -->
      <div
        v-for="n in 20"
        :key="n"
        :class="n % 2 === 1 ? 'type-line odd' : 'type-line even'"
      >
        JOIN THE CULT JOIN THE CULT JOIN THE CULT JOIN THE CULT JOIN THE CULT
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
  const TYPE_LINE_OPACITY = 0.99; //opacity aanpassing

  gsap.set(oddLines, { opacity: TYPE_LINE_OPACITY });
  gsap.set(evenLines, { opacity: TYPE_LINE_OPACITY });

  const timeline = gsap.timeline({ repeat: -1, defaults: { ease: "customEase" } });
  timeline.to(kineticEl, { duration: 1.4, scale: 2.7, rotation: -90 })
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
  display: grid;
  place-items: center;
}

#kinetic-type {
  position: relative;
  display: grid;
  place-items: center;
  font-weight: 800;
  font-size: clamp(3rem, 10vw, 12rem);
  white-space: nowrap;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  will-change: transform, opacity;
  pointer-events: none;
  z-index: 10;
  grid-auto-rows: 1; /* Maak rijhoogte strak */
  gap: 0; /* Geen ruimte tussen rijen */
}


.type-line {
  opacity: 0.15;
  will-change: transform, opacity;
  white-space: nowrap;
  color: white;
  line-height: 1; /* Strakke verticale spacing */
  margin: 0;
  padding: 0;
}

.type-line.odd {
  color: #eee;
}

.type-line.even {
  color: #ddd;
}
</style>






