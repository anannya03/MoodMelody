<template>
  <div class="mt-5 container">
    <div class="buttons is-centered">
      <div @mouseup="attackChange">
        <p class="custom-text-dark custom-regular-text">A</p>
        <VueCircleSlider
          v-model="customAttack"
          :circle-width="4"
          :progress-width="6"
          :knob-radius="6"
          :side="60"
          circle-color="#803A61"
          progress-color="#C92C6D"
          knob-color="#C92C6D"
        />
      </div>
      <div @mouseup="decayChange">
        <p class="custom-text-dark custom-regular-text">D</p>
        <VueCircleSlider
          v-model="customDecay"
          :circle-width="4"
          :progress-width="6"
          :knob-radius="6"
          :side="60"
          circle-color="#803A61"
          progress-color="#C92C6D"
          knob-color="#C92C6D"
        />
      </div>
      <div @mouseup="sustainChange">
        <p class="custom-text-dark custom-regular-text">S</p>
        <VueCircleSlider
          v-model="customSustain"
          :circle-width="4"
          :progress-width="6"
          :knob-radius="6"
          :side="60"
          circle-color="#803A61"
          progress-color="#C92C6D"
          knob-color="#C92C6D"
        />
      </div>
      <div @mouseup="releaseChange">
        <p class="custom-text-dark custom-regular-text">
          R
        </p>
        <VueCircleSlider
          v-model="customRelease"
          :circle-width="4"
          :progress-width="6"
          :knob-radius="6"
          :side="60"
          circle-color="#803A61"
          progress-color="#C92C6D"
          knob-color="#C92C6D"
        />
      </div>
    </div>
    <div class="buttons is-centered">
      <button class="button" @click="sineOscillatorClick">
        <span class="icon">
          <img class="is-large" src="../../public/sine-wave.svg" />
        </span>
      </button>
      <button class="button" @click="squareOscillatorClick">
        <span class="icon">
          <img class="is-large" src="../../public/square-wave.svg" />
        </span>
      </button>
      <button class="button" @click="triangleOscillatorClick">
        <span class="icon">
          <img class="is-large" src="../../public/triangle-wave.svg" />
        </span>
      </button>
      <button class="button" @click="sawtoothOscillatorClick">
        <span class="icon">
          <img class="is-large" src="../../public/sawtooth-wave.svg" />
        </span>
      </button>
    </div>
  </div>
</template>

<script>
import VueCircleSlider from "../../node_modules/vue-circle-slider/src/components/CircleSlider";

export default {
  name: "Controls",
  components: { VueCircleSlider },
  data: () => ({
    customAttack: 10,
    customDecay: 75,
    customSustain: 35,
    customRelease: 10,
  }),
  methods: {
    // send custom events with the oscillators that were clicked
    sineOscillatorClick() {
      this.$emit("oscillator-click-event", "sine");
    },
    squareOscillatorClick() {
      this.$emit("oscillator-click-event", "square");
    },
    triangleOscillatorClick() {
      this.$emit("oscillator-click-event", "triangle");
    },
    sawtoothOscillatorClick() {
      this.$emit("oscillator-click-event", "sawtooth");
    },
    attackChange() {
      console.log("Attack was changed.");
      this.$emit("attack-change-event", this.customAttack);
    },
    sustainChange() {
      console.log("Sustain was changed.");
      this.$emit("sustain-change-event", this.customSustain);
    },
    decayChange() {
      console.log("Decay was changed.");
      this.$emit("decay-change-event", this.customDecay);
    },
    releaseChange() {
      console.log("Release was changed.");
      this.$emit("release-change-event", this.customRelease);
    },
  },
};
</script>

<style scoped>
.button {
  border: none;
  background-color: #E09F3E; /* Mustard Yellow */
    color: #FFFFFF; /* White */
    box-shadow: 0 4px 6px rgba(181, 123, 36, 0.6);
    cursor: pointer;
    transition: background-color 0.3s ease, box-shadow 0.3s ease, transform 0.1s ease;
}
.button:hover {
  background-color: #BC6C25; /* Darker Mustard Yellow */
    box-shadow: 0 6px 8px rgba(181, 123, 36, 0.8);
}
.button:active {
  background-color: #9C6615; /* Even Darker Mustard Yellow */
    box-shadow: 0 2px 4px rgba(181, 123, 36, 0.8); /* Darker Soft Brown */
    transform: translateY(2px);
}
.is-large {
  height: 100%;
  width: 100%;
}
</style>
