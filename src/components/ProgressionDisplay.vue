<template>
  <div class="mt-5 container is-centered has-text-centered">
    <!-- Display message when progression is null or undefined -->
    <span
      class="custom-text-dark custom-regular-text notif"
      v-if="progression === null || progression === undefined"
    >
      Select a Mood above to get the Progression.
    </span>
    
    <!-- Display message when server is unreachable -->
    <span
      class="custom-text-dark custom-regular-text notif"
      v-else-if="progression === 'NA'"
    >
      Server unreachable :/ Please try again later.
    </span>
    
    <!-- Display the progression when it is available -->
    <span class="custom-text-dark custom-regular-text notif" v-else>
      Here's a progression for you:
      <strong class="text">{{ convertToRoman(progression) }}</strong>
    </span>
  </div>
</template>

<script>
export default {
  name: "ProgressionDisplay",
  props: ["progression"],
  watch: {
    progression(newVal) {
      console.log("Progression updated in ProgressionDisplay:", newVal);
    }
  },
  methods: {
    convertToRoman(progression) {
      if (!progression) {
        return "";
      }

      var romanArray = [];
      progression.forEach((number) => {
        switch (number) {
          case "1":
            romanArray.push("I");
            break;
          case "2":
            romanArray.push("ii");
            break;
          case "3":
            romanArray.push("iii");
            break;
          case "4":
            romanArray.push("IV");
            break;
          case "5":
            romanArray.push("V");
            break;
          case "6":
            romanArray.push("vi");
            break;
          default:
            break;
        }
      });
      return romanArray.join("-");
    },
  },
};
</script>

<style scoped>
.chord-display {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  box-shadow: -0.3rem 0.3rem 0 0 #ece8d9;
  border: none;
  background-color: #fffdf6;
  color: #3D3D3D;
}
.text {
  color: #3D3D3D;
}
.notif {
  color: #C92C6D;
  font-weight: 650;
  font-size: 16px;
}
</style>
