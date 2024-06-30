<template>
  <div
    class="key"
    v-bind:class="{
      'black-key': pianoKey.type === 'black',
      'white-key': pianoKey.type === 'white',
    }"
    @mousedown="keyClick"
  ></div>
</template>

<script>
export default {
  name: "Key",
  props: ["pianoKey"],
  methods: {
    keyClick() {
      // send a custom event with the piano key that was clicked
      this.$emit("key-click-event", this.pianoKey);
    },
  },
};
</script>

<style>
.black-key {
  width: 35px;
  height: 140px;
  background-color: #4A4A4A;
  z-index: 1;
  position: absolute;
  margin-top: -234px;
  margin-left: -18px;
}
.white-key {
  width: 55px;
  height: 234px;
  background-color: #fff;
}
.key {
  display: inline-block;
  padding: 10%;
  border-radius: 4px;
  box-shadow: -0.3rem 0.3rem 0 0 #F4ECD8;
}
.key:active {
  box-shadow: none;
}

@media only screen and (max-width: 480px),
  only screen and (max-device-width: 480px) {
  .black-key {
    width: 18px;
    height: 100px;
    background-color:#4A4A4A;
    z-index: 1;
    position: absolute;
    margin-top: -169px;
    margin-left: -13px;
  }
  .white-key {
    width: 25px;
    height: 170px;
    background-color:#fff;
  }
}
@media only screen and (min-width: 481px) and (max-width: 550px) {
  .black-key {
    width: 20px;
    height: 120px;
    background-color: #4A4A4A;
    z-index: 1;
    position: absolute;
    margin-top: -200px;
    margin-left: -15px;
  }
  .white-key {
    width: 30px;
    height: 200px;
    background-color: #fff;
  }
}
@media only screen and (min-width: 551px) and (max-width: 680px) {
  .black-key {
    width: 28px;
    height: 120px;
    background-color: #4A4A4A;
    z-index: 1;
    position: absolute;
    margin-top: -200px;
    margin-left: -15px;
  }
  .white-key {
    width: 38px;
    height: 200px;
    background-color: #fff;
  }
}

@media only screen and (min-width: 681px) and (max-width: 747px) {
  .black-key {
    width: 25px;
    height: 120px;
    background-color: #4A4A4A;
    z-index: 1;
    position: absolute;
    margin-top: -200px;
    margin-left: -15px;
  }
  .white-key {
    width: 45px;
    height: 200px;
    background-color: #fff;
  }
}
@media only screen and (max-width: 388px) {
  .black-key {
    width: 14px;
    height: 80px;
    background-color: #4A4A4A;
    z-index: 1;
    position: absolute;
    margin-top: -130px;
    margin-left: -10px;
  }
  .white-key {
    width: 18px;
    height: 130px;
    background-color: #fff;
  }
}
</style>
