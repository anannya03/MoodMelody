<template>
  <!-- Piano contianer -->
  <div class="mt-5 container has-text-centered">
    <!-- Display controls -->
    <Controls
      class="mb-5"
      v-on:oscillator-click-event="handleOscillatorClick"
      v-on:attack-change-event="handleAttackChange"
      v-on:sustain-change-event="handleSustainChange"
      v-on:decay-change-event="handleDecayChange"
      v-on:release-change-event="handleReleaseChange"
    />
    <!-- Loop through all the keys -->
    <div class="key-container" v-for="key in keys" :key="key.id">
      <Key v-bind:pianoKey="key" v-on:key-click-event="handleKeyClick" />
    </div>
    <!-- Display MoodSelector -->
    <MoodSelector v-on:mood-click-event="handleMoodSelection" />
    <!-- Display generated progression by sending the progression as a prop to the component -->
    <ProgressionDisplay v-bind:progression="progression" />
  </div>
</template>

<script>
import Key from "./Key";
import MoodSelector from "./MoodSelector";
import * as Tone from "tone";
import Controls from "./Controls";
import ProgressionDisplay from "./ProgressionDisplay";

export default {
  name: "Piano",
  components: { Key, Controls, MoodSelector, ProgressionDisplay },
  data: () => ({
    synth: new Tone.Synth({
      oscillator: {
        type: "sine",
      },
      envelope: {
        // attack goes from 0 to 1 in steps of 0.01
        attack: 0.1,

        // decay goes from 0 to 1 in steps of 0.01
        decay: 0.75,

        // sustain goes from 0 to 1 in steps of 0.01
        sustain: 0.35,

        // release goes from 0 to 1 in steps of 0.01
        release: 0.1,
      },
    }),
    progression: null,
    keys: [
      {
        id: 1,
        keyName: "C",
        type: "white",
        character: "A",
      },
      {
        id: 2,
        keyName: "C#",
        type: "black",
        character: "W",
      },
      {
        id: 3,
        keyName: "D",
        type: "white",
        character: "S",
      },
      {
        id: 4,
        keyName: "D#",
        type: "black",
        character: "E",
      },
      {
        id: 5,
        keyName: "E",
        type: "white",
        character: "D",
      },
      {
        id: 6,
        keyName: "F",
        type: "white",
        character: "F",
      },
      {
        id: 7,
        keyName: "F#",
        type: "black",
        character: "T",
      },
      {
        id: 8,
        keyName: "G",
        type: "white",
        character: "G",
      },
      {
        id: 9,
        keyName: "G#",
        type: "black",
        character: "Y",
      },
      {
        id: 10,
        keyName: "A",
        type: "white",
        character: "H",
      },
      {
        id: 11,
        keyName: "A#",
        type: "black",
        character: "U",
      },
      {
        id: 12,
        keyName: "B",
        type: "white",
        character: "J",
      },
      {
        id: 13,
        keyName: "C",
        type: "white",
        character: "A",
      },
      {
        id: 14,
        keyName: "C#",
        type: "black",
        character: "W",
      },
      {
        id: 15,
        keyName: "D",
        type: "white",
        character: "S",
      },
      {
        id: 16,
        keyName: "D#",
        type: "black",
        character: "E",
      },
      {
        id: 17,
        keyName: "E",
        type: "white",
        character: "D",
      },
      {
        id: 18,
        keyName: "F",
        type: "white",
        character: "F",
      },
      {
        id: 19,
        keyName: "F#",
        type: "black",
        character: "T",
      },
      {
        id: 20,
        keyName: "G",
        type: "white",
        character: "G",
      },
    ],
  }),
  created() {
        console.log("Initial progression:", this.progression);

    const audioContext = Tone.context;

    const resumeAudioContext = () => {
        if (audioContext.state === "suspended") {
          audioContext.resume();
        }
      };

    // listen for keypresses and play the corresponding sounds
    window.addEventListener("keydown", (event) => {
      resumeAudioContext();
      if (event.defaultPrevented) {
        // do nothing if the event was already processed
        return;
      }

      // get the Unicode value of the pressed key
      var pressedKeyCode = event.keyCode;

      // convert the Unicode value to ASCII
      var pressedCharacter = String.fromCharCode(pressedKeyCode);

      var pianoKey = this.keys.filter(function(e) {
        return e.character === pressedCharacter;
      });
      try {
        // play the sound for the pressed key
        this.synth.toDestination();
        this.synth.triggerAttackRelease(pianoKey[0].keyName + "4", "8n");
      } catch (err) {
        console.log(err);
      }

      // cancel the default action to avoid it being handled twice
      event.preventDefault();
    });
  },
  methods: {
    handleKeyClick(pianoKey) {
      // play sound from the clicked key
    const audioContext = Tone.context;
    if (audioContext.state === "suspended") {
      audioContext.resume();
    }

    this.synth.toDestination();
    this.synth.triggerAttackRelease(pianoKey.keyName + "4", "8n");
    },
    handleOscillatorClick(newOscillator) {
      // change the oscillator on click to the new oscillator
      this.synth.oscillator.type = newOscillator;

      // force update to reflect changes
      this.$forceUpdate();
    },
    handleAttackChange(customAttack) {
      this.synth.envelope.attack = customAttack / 100;
      this.$forceUpdate();
    },
    handleSustainChange(customSustain) {
      this.synth.envelope.sustain = customSustain / 100;
      this.$forceUpdate();
    },
    handleDecayChange(customDecay) {
      this.synth.envelope.decay = customDecay / 100;
      this.$forceUpdate();
    },
    handleReleaseChange(customRelease) {
      this.synth.envelope.release = customRelease / 100;
      this.$forceUpdate();
    },
    handleMoodSelection(mood) {
      console.log(mood);
      var baseURL =
        "https://chordpro.wl.r.appspot.com/api/filter?";

      // assign valence and energy to moods
      var valence = 0,
        energy = 0;
      if (mood === "happy") {
        valence = 0.6;
        energy = 0.8;
      } else if (mood === "calm") {
        valence = 0.6;
        energy = 0.5;
      } else if (mood === "anxious") {
        valence = 0.4;
        energy = 0.7;
      } else {
        valence = 0.3;
        energy = 0.5;
      }

      // new enpoint with valence and energy
      const modifiedURL = baseURL + "valence=" + valence + "&energy=" + energy;

      // method to generate a chord array from the number notation in a key
      function generateChordArray(number) {
        var chordArray = [];
        switch (number) {
          case "1":
            chordArray = ["C4", "E4", "A4"];
            break;
          case "2":
            chordArray = ["D4", "F4", "A4"];
            break;
          case "3":
            chordArray = ["E4", "G4", "B4"];
            break;
          case "4":
            chordArray = ["F4", "A5", "C5"];
            break;
          case "5":
            chordArray = ["G4", "B5", "D5"];
            break;
          case "6":
            chordArray = ["A4", "C5", "E5"];
            break;
          case "7":
            chordArray = ["B4", "D5", "F5"];
            break;

          default:
            break;
        }
        return chordArray;
      }

      // define calling method
      const getData = async (url) => {
        try {
          const response = await fetch(url);
          const json = await response.json();
          const randomChordProgression =
            json[Math.floor(Math.random() * json.length)];

          // get the numeric value of the random progression for the selected mood
          this.progression = randomChordProgression.child_path.split(",");

          // initialise polysynth
          const polySynth = new Tone.PolySynth().toDestination();
          const synthOptions = {
            oscillator: {
              type: this.synth.oscillator.type,
            },
            envelope: {
              attack: this.synth.envelope.attack,
              delay: this.synth.envelope.delay,
              sustain: this.synth.envelope.sustain,
              release: this.synth.envelope.release,
            },
          };
          polySynth.set(synthOptions);

          // initialise current time
          const now = Tone.now();

          // play the received four chords in a loop
          for (let i = 0; i < 4; i++) {
            polySynth.triggerAttackRelease(
              generateChordArray(this.progression[i]),
              "8n",
              now + i
            );
          }

          // force update to reflect changes
          this.$forceUpdate();
          console.log(this.progression);
        } catch (error) {
          console.log(error);

          // set progression as NA so that an error message can be displayed.
          this.progression = "NA";
        }
      };

      // make API call based on valence and energy
      getData(modifiedURL);
    },
  },
};
</script>

<style scoped>
.key-container {
  padding: 1px !important;
  margin: 0px !important;
  max-width: 50% !important;
  flex-grow: unset !important;
  display: inline-block;
  position: relative;
}
</style>
