<template>
  <div class="mt-5 container">
    <div class="buttons is-centered">
      <!-- Guide button -->
      <a class="button" @click="isGuideActive = true">
        <span class="is-large mr-2">
          <i class="fas fa-info-circle "></i>
        </span>
        <span class="custom-regular-text">Guide</span>
      </a>
      <!-- Github button -->
      <a
        class="button"
        href="https://github.com/anannya03/MoodMelody"
      >
        <span class="is-large mr-2">
          <i class="fab fa-github" style="white"></i>
        </span>
        <span class="custom-regular-text">Source</span>
      </a>
    </div>
    <!-- Display the guide if isGuideActive is true -->
    <div class="modal" v-bind:class="{ 'is-active': isGuideActive }">
      <div
        class="modal-background"
        @click="isGuideActive = !isGuideActive"
      ></div>
      <div class="modal-content">
        <div class="notification custom-notification custom-text-dark">
          <button
            class="delete"
            aria-label="close"
            @click="isGuideActive = !isGuideActive"
          ></button>
          <strong>
            <span class="notif">Hey there! Here's a quick guide on using this project.</span>
          </strong>
          <br /><br />
          1. Click on the keys or use your keyboard to play sounds. The keys are
          mapped as follows: <br/>
          <strong><span class="notif">a - C, w - C#, s - D, e - D#, d - E, f - F, t - F#, g - G, y - G#,
            h - A, u - A#, j - B</span></strong>.
          <br /><br/>
          2. Click on the waveform buttons to toggle between the sine, square,
          triangle and sawtooth waveforms.
          <br /><br/>
          3. Move the sliders to modify the ADSR(Attack-Delay-Sustain-Release)
          envelope. For more information about <strong>ADSR</strong> envelopes,
          click
          <a href="https://en.wikipedia.org/wiki/Envelope_(music)"><strong><span class="notif">here</span></strong></a>.
          <br /><br/>
          4. Choose a mood from the 4 given options to get chord progression
          suggestions. The chord are mapped according to the roman numeral chord
          notation in a particular key.
          <br />
          <br />
          <strong><center><span class="notif center">Have Fun with Music Composition!</span></center></strong>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Info",
  data: function() {
    return {
      isGuideActive: true,
    };
  },
};
</script>

<style scoped>
.button {
  border: none;
box-shadow: 0 4px 6px rgba(181, 123, 36, 0.6);
  background-color: #E09F3E; /* Mustard Yellow */
  color: #FFFFFF; 
  cursor: pointer;
    transition: background-color 0.3s ease, box-shadow 0.3s ease, transform 0.1s ease;
}
.button:hover{
  background-color: #BC6C25; /* Darker Mustard Yellow */
    box-shadow: 0 6px 8px rgba(181, 123, 36, 0.8); 
}
.button:focus {
  border: none;
  box-shadow: -0.3rem 0.3rem 0 0 #F4ECD8;
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
.custom-notification {
  background-color: #F4ECD8;
}
.notif{
  color:#C92C6D;
}

</style>
