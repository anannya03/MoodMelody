<template>
  <div class="mt-5 container">
    <div class="buttons is-centered ">
      <button
        class="button custom-text-dark custom-regular-text"
        @click="happyButtonClick"
      >
        Happy
      </button>
      <button
        class="button custom-text-dark custom-regular-text"
        @click="calmButtonClick"
      >
        Calm
      </button>
      <button
        class="button custom-text-dark custom-regular-text"
        @click="sadButtonClick"
      >
        Sad
      </button>
      <button
        class="button custom-text-dark custom-regular-text"
        @click="anxiousButtonClick"
      >
        Anxious
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MoodSelector",
  methods: {
    happyButtonClick() {
      this.$emit("mood-click-event", "happy");
    },
    sadButtonClick() {
      this.$emit("mood-click-event", "sad");
    },
    calmButtonClick() {
      this.$emit("mood-click-event", "calm");
    },
    anxiousButtonClick() {
      this.$emit("mood-click-event", "anxious");
    },
  },
};
</script>

<style scoped>
.button {
  border: none;
  box-shadow: 0 4px 6px rgba(181, 123, 36, 0.6);
  background-color: #E09F3E;
  color: #FFFFFF; /* White */
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease, transform 0.1s ease;
}

   
    
.button:hover {
  background-color: #BC6C25; /* Darker Mustard Yellow */
  box-shadow: 0 6px 8px rgba(181, 123, 36, 0.8); 
  /*background-color: #9C6615;
  color: #fff; */
}
.button:focus {
  border: none;
  box-shadow: -0.3rem 0.3rem 0 0 #F4ECD8;
}
.button:active {
    background-color: #9C6615; /* Even Darker Mustard Yellow */
    box-shadow: 0 2px 4px rgba(181, 123, 36, 0.8); /* Darker Soft Brown */
    transform: translateY(2px); /* Slight movement for a pressed effect */
}
.is-large {
  height: 100%;
  width: 100%;
}
</style>
