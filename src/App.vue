<template>
  <div id="app">
    <div class="background-frame"></div>

    <div
      v-for="item in textItems"
      :key="item.id"
      class="text-item"
      :ref="'textItem' + item.id"
      :style="itemStyle(item)"
      :class="{ highlight: item.highlighted || autoHighlightActive }"
      @mouseenter="onHover(item.id)"
      @mouseleave="onLeave(item.id)"
      :data-text="item.text"
    >
      {{ item.text }}
    </div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrambleTextPlugin } from "gsap/ScrambleTextPlugin";
gsap.registerPlugin(ScrambleTextPlugin);

export default {
  name: "App",
  data() {
    return {
      textItems: [
        { id: 1, text: "BE", top: "5%", left: "8%", right: null, highlighted: false, scrambleTl: null },
        { id: 2, text: "PRESENT", top: "5%", left: "15%", right: null, highlighted: false, scrambleTl: null },
        { id: 3, text: "LISTEN", top: "5%", left: "28%", right: null, highlighted: false, scrambleTl: null },
        { id: 4, text: "DEEPLY", top: "5%", left: "42%", right: null, highlighted: false, scrambleTl: null },
        { id: 5, text: "OBSERVE", top: "5%", left: "55%", right: null, highlighted: false, scrambleTl: null },
        { id: 6, text: "&", top: "5%", left: "75%", right: null, highlighted: false, scrambleTl: null },
        { id: 7, text: "FEEL", top: "5%", left: "85%", right: null, highlighted: false, scrambleTl: null },
        { id: 8, text: "MAKE", top: "10%", left: "12%", right: null, highlighted: false, scrambleTl: null },
        { id: 9, text: "BETTER", top: "10%", left: "45%", right: null, highlighted: false, scrambleTl: null },
        { id: 10, text: "DECISIONS", top: "10%", left: null, right: "20%", highlighted: false, scrambleTl: null },
        { id: 11, text: "THE", top: "15%", left: "8%", right: null, highlighted: false, scrambleTl: null },
        { id: 12, text: "CREATIVE", top: "15%", left: "30%", right: null, highlighted: false, scrambleTl: null },
        { id: 13, text: "PROCESS", top: "15%", left: "55%", right: null, highlighted: false, scrambleTl: null },
        { id: 14, text: "IS", top: "15%", left: null, right: "20%", highlighted: false, scrambleTl: null },
        { id: 15, text: "MYSTERIOUS", top: "15%", left: null, right: "5%", highlighted: false, scrambleTl: null },
        { id: 16, text: "S", top: "25%", left: "5%", right: null, highlighted: false, scrambleTl: null },
        { id: 17, text: "I", top: "25%", left: "10%", right: null, highlighted: false, scrambleTl: null },
        { id: 18, text: "M", top: "25%", left: "15%", right: null, highlighted: false, scrambleTl: null },
        { id: 19, text: "P", top: "25%", left: "20%", right: null, highlighted: false, scrambleTl: null },
        { id: 20, text: "L", top: "25%", left: "25%", right: null, highlighted: false, scrambleTl: null },
        { id: 21, text: "I", top: "25%", left: "30%", right: null, highlighted: false, scrambleTl: null },
        { id: 22, text: "C", top: "25%", left: "35%", right: null, highlighted: false, scrambleTl: null },
        { id: 23, text: "I", top: "25%", left: "40%", right: null, highlighted: false, scrambleTl: null },
        { id: 24, text: "T", top: "25%", left: "45%", right: null, highlighted: false, scrambleTl: null },
        { id: 25, text: "Y", top: "25%", left: "50%", right: null, highlighted: false, scrambleTl: null },
        { id: 26, text: "IS THE KEY", top: "25%", left: null, right: "5%", highlighted: false, scrambleTl: null },
        { id: 27, text: "FIND YOUR VOICE", top: "35%", left: "25%", right: null, highlighted: false, scrambleTl: null },
        { id: 28, text: "TRUST INTUITION", top: "35%", left: "65%", right: null, highlighted: false, scrambleTl: null },
        { id: 29, text: "EMBRACE SILENCE", top: "50%", left: "5%", right: null, highlighted: false, scrambleTl: null },
        { id: 30, text: "QUESTION EVERYTHING", top: "50%", left: null, right: "5%", highlighted: false, scrambleTl: null },
        { id: 31, text: "TRUTH", top: "75%", left: "20%", right: null, highlighted: false, scrambleTl: null },
        { id: 32, text: "WISDOM", top: "75%", left: null, right: "20%", highlighted: false, scrambleTl: null },
        { id: 33, text: "FOCUS", top: "80%", left: "10%", right: null, highlighted: false, scrambleTl: null },
        { id: 34, text: "ATTENTION", top: "80%", left: "35%", right: null, highlighted: false, scrambleTl: null },
        { id: 35, text: "AWARENESS", top: "80%", left: "65%", right: null, highlighted: false, scrambleTl: null },
        { id: 36, text: "PRESENCE", top: "80%", left: null, right: "10%", highlighted: false, scrambleTl: null },
        { id: 37, text: "SIMPLIFY", top: "85%", left: "25%", right: null, highlighted: false, scrambleTl: null },
        { id: 38, text: "REFINE", top: "85%", left: null, right: "25%", highlighted: false, scrambleTl: null },
      ],
      autoHighlightActive: false,
      autoHighlightInterval: null,
      autoHighlightTimeout: null,
      userHoveringId: null,
      scrambleIntervals: [],
    };
  },
  methods: {
    itemStyle(item) {
      return {
        top: item.top,
        left: item.left,
        right: item.right,
        position: "absolute",
      };
    },

    startScramble(item, el) {
      if (item.scrambleTl) return; // al actief

      item.scrambleTl = gsap.to(el, {
        duration: 1.2,
        scrambleText: {
          text: item.text,
          chars: "■▪▌▐▬",
          revealDelay: 0.5,
          speed: 0.3, //glitch speed
        },
        ease: "none",
        repeat: -1,
        yoyo: true,
        repeatDelay: 2,
      });
    },

    stopScramble(item) {
      if (item.scrambleTl) {
        item.scrambleTl.kill();
        item.scrambleTl = null;
      }
    },

    onHover(id) {
      this.userHoveringId = id;
      this.clearAutoHighlight();

      const item = this.textItems.find(i => i.id === id);
      if (item) {
        item.highlighted = true;
        const el = this.$refs["textItem" + id];
        if (el && el[0]) this.startScramble(item, el[0]);
      }
    },

    onLeave(id) {
      this.userHoveringId = null;

      const item = this.textItems.find(i => i.id === id);
      if (item) {
        item.highlighted = false;
        this.stopScramble(item);
      }

      this.startAutoHighlight();
    },

    startAutoHighlight() {
      if (this.autoHighlightInterval) return;

      // Rechthoek animatie, alle items tegelijk
      this.autoHighlightInterval = setInterval(() => {
        this.autoHighlightActive = true;

        this.autoHighlightTimeout = setTimeout(() => {
          this.autoHighlightActive = false;
        }, 1000); // rechthoek highlight duur

      }, 5000); // interval rechthoek animatie
    },

    clearAutoHighlight() {
      this.autoHighlightActive = false;
      if (this.autoHighlightInterval) {
        clearInterval(this.autoHighlightInterval);
        this.autoHighlightInterval = null;
      }
      if (this.autoHighlightTimeout) {
        clearTimeout(this.autoHighlightTimeout);
        this.autoHighlightTimeout = null;
      }
    },

    startRandomScrambles() {
      // Zorg dat eerder gestarte intervals weg zijn
      this.scrambleIntervals.forEach(i => clearInterval(i));
      this.scrambleIntervals = [];

      // Per item random scramble starten en stoppen met eigen timing
      this.textItems.forEach(item => {
        const el = this.$refs["textItem" + item.id];
        if (!el || !el[0]) return;
        const element = el[0];

        // Interval met random delay tussen 4-12 sec
        const interval = setInterval(() => {
          // Niet scrambelen als user hovered op dat item
          if (this.userHoveringId === item.id) return;

          this.startScramble(item, element);

          // Stop scramble na random duur 1-3 sec
          setTimeout(() => {
            this.stopScramble(item);
          }, 1000 + Math.random() * 2000);
        }, 4000 + Math.random() * 8000);

        this.scrambleIntervals.push(interval);
      });
    },

    stopAllScrambles() {
      this.textItems.forEach(item => this.stopScramble(item));
      this.scrambleIntervals.forEach(i => clearInterval(i));
      this.scrambleIntervals = [];
    },
  },

  mounted() {
    this.startAutoHighlight();
    this.startRandomScrambles();
  },

  beforeUnmount() {
    this.clearAutoHighlight();
    this.stopAllScrambles();
  },
};
</script>

<style scoped>
@font-face {
  font-family: "InterTight";
  src: url("/InterTight.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}

#app {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: #000;
  font-family: "InterTight", sans-serif;
  overflow: hidden;
}

.background-frame {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #000;
  background-size: 100% 100%;
  background-position: center;
  z-index: 0;
  pointer-events: none;
}

.text-item {
  color: #838383;
  font-size: 0.8rem;
  text-transform: uppercase;
  opacity: 0.8;
  white-space: nowrap;
  font-family: "InterTight", monospace;
  z-index: 2;
  cursor: pointer;
  user-select: none;
  position: absolute;
  transition: color 0.3s ease;
  --highlight-width: 0;
}

.text-item::after {
  content: "";
  position: absolute;
  top: -2px;
  left: -4px;
  width: 0;
  height: calc(100% + 4px);
  background-color: #ffe1eb;
  z-index: -1;
  transition: width 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
  will-change: width;
  pointer-events: none;
}

.text-item.highlight {
  color: #000000 !important;
}

.text-item.highlight::after {
  width: calc(100% + 8px) !important;
  transition-timing-function: cubic-bezier(0.34, 1.56, 0.64, 1) !important;
}
</style>




