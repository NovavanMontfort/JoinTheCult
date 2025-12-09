<template>
  <div class="keyboard">
    <span class="key">J</span>
    <span class="key">O</span>
    <span class="key">I</span>
    <span class="key">N</span>
    <span class="key">T</span>
    <span class="key">H</span>
    <span class="key">E</span>
    <span class="key">C</span>
    <span class="key">U</span>
    <span class="key">L</span>
    <span class="key">T</span>
  </div>

</template>

<script setup>
// Geen extra script nodig voor deze statische animatie
</script>

<style>
  @font-face {
  font-family: 'Inter Tight';
  src: url('/InterTight.ttf') format('truetype');
  font-weight: 900;
  font-style: normal;
  font-display: swap;
}
/* Body styles niet toepassen scoped, maar hier simuleer ik ze op root element */
:root {
  background-color: #101013;
  color: #fff;
  font-family: 'Inter Tight', sans-serif;
  font-weight: 900;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  margin: 0;
}

.keyboard {
  white-space: nowrap;
  display: flex;
  justify-content: center;
  gap: 0.3em; 
}

.key {
  display: block;
  font-size: 15vw;
  letter-spacing: -1vw;
  transition: transform 0.2s;
}


/* Animaties */
@keyframes pressDown1 {
  30%, 40%, 100% { transform: translateY(0); }
  35% { transform: translateY(10px); }
}
@keyframes pressDown2 {
  70%, 80%, 100% { transform: translateY(0); }
  75% { transform: translateY(10px); }
}
@keyframes pressDown3 {
  30%, 40%, 100% { transform: translateY(0); }
  35% { transform: translateY(10px); }
}
@keyframes pressDown4 {
  40%, 50%, 100% { transform: translateY(0); }
  45% { transform: translateY(10px); }
}
@keyframes pressDown5 {
  20%, 30%, 100% { transform: translateY(0); }
  25% { transform: translateY(10px); }
}
@keyframes pressDown6 {
  60%, 70%, 100% { transform: translateY(0); }
  65% { transform: translateY(10px); }
}
@keyframes pressDown7 {
  10%, 20%, 100% { transform: translateY(0); }
  15% { transform: translateY(10px); }
}
@keyframes pressDown8 {
  35%, 45%, 100% { transform: translateY(0); }
  40% { transform: translateY(10px); }
}

/* Animatie per letter */
.key:nth-child(1) { animation: pressDown1 2s infinite; }
.key:nth-child(2) { animation: pressDown2 3s infinite; }
.key:nth-child(3) { animation: pressDown3 4s infinite; }
.key:nth-child(4) { animation: pressDown4 2.5s infinite; }
.key:nth-child(5) { animation: pressDown5 2.5s infinite; }
.key:nth-child(6) { animation: pressDown6 3.5s infinite; }
.key:nth-child(7) { animation: pressDown7 2.2s infinite; }
.key:nth-child(8) { animation: pressDown8 3.2s infinite; }

/* Extra links */
.jux-linx {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 10px;
  position: absolute;
  left: 20px;
  bottom: 20px;
}

a {
  text-decoration: none;
  font-family: 'Inter Tight', sans-serif;
  font-weight: 900; /* Bold */
  font-size: 16px;
  color: white;
  background-color: black;
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  padding: 5px 10px;
  transition: all 0.1s ease-in;
}

</style>



