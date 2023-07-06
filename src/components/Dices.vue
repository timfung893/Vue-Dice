<template>
  <div class="dice-wrapper">
    <div class="dice" id="dice-1">
      <div class="spinner" v-bind:class="'dice-' + dices[0]">
        <div class="face1">1</div>
        <div class="face2">2</div>
        <div class="face3">3</div>
        <div class="face4">4</div>
        <div class="face5">5</div>
        <div class="face6">6</div>
      </div>
    </div>
    <div class="dice" id="dice-2">
      <div class="spinner" v-bind:class="'dice-' + dices[1]">
        <div class="face1">1</div>
        <div class="face2">2</div>
        <div class="face3">3</div>
        <div class="face4">4</div>
        <div class="face5">5</div>
        <div class="face6">6</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dices",
  props: {
    dices: { type: Array, default: [2, 2] },
  },
  data() {
    return {};
  },
};
</script>

<style scoped>
#dice-1 {
  top: 121px;
}
#dice-2 {
  top: 250px;
}
.dice {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 120px;
  height: 120px;
  box-shadow: 0px 10px 60px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}
.spinner {
  transform-style: preserve-3d;
  transform-origin: 60px 60px 0;
  transition: all 0.9s ease;
  transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
}
.spinner div {
  position: absolute;
  width: 120px;
  height: 120px;
  font-size: 0;
  text-align: center;
  transition: all 0.3s ease;
  border: 1px solid #ccc;
  border-radius: 5px;
  opacity: 1;
  box-shadow: 0px 10px 60px rgba(0, 0, 0, 0.1);
}
.spinner .face1 {
  background-image: url("/public/assets/dice-1.png");
  background-position: center;
  background-size: cover;
  transform: translateZ(60px);
}
.spinner .face2 {
  background-image: url("/public/assets/dice-2.png");
  background-position: center;
  background-size: cover;
  transform: rotateY(90deg) translateZ(60px);
}
.spinner .face3 {
  background-image: url("/public/assets/dice-3.png");
  background-position: center;
  background-size: cover;
  transform: rotateY(90deg) rotateX(90deg) translateZ(60px);
}
.spinner .face4 {
  background-image: url("/public/assets/dice-4.png");
  background-position: center;
  background-size: cover;
  transform: rotateY(180deg) rotateZ(90deg) translateZ(60px);
}
.spinner .face5 {
  background-image: url("/public/assets/dice-5.png");
  background-position: center;
  background-size: cover;
  transform: rotateY(-90deg) rotateZ(90deg) translateZ(60px);
}
.spinner .face6 {
  background-image: url("/public/assets/dice-6.png");
  background-position: center;
  background-size: cover;
  transform: rotateX(-90deg) translateZ(60px);
}
.spinner.dice-1 {
  transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
}
 .spinner.dice-2 {
  transform: rotateX(0deg) rotateY(-90deg) rotateZ(0deg);
} 
.spinner.dice-3 {
  transform: rotateX(0deg) rotateY(-90deg) rotateZ(90deg);
}
.spinner.dice-4 {
  transform: rotateX(0deg) rotateY(180deg) rotateZ(90deg);
}
.spinner.dice-5 {
  transform: rotateX(0deg) rotateY(90deg) rotateZ(0deg);
}
.spinner.dice-6 {
  transform: rotateX(90deg) rotateY(90deg) rotateZ(0deg);
}
</style>
