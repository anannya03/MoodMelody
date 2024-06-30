<template>
  <div class="section is-vcentered">
    <Heading />
    <Piano />
    <!-- <Instruction /> -->
    <Links />
  </div>
</template>

<script>
import "./../node_modules/bulma/css/bulma.css";
import Heading from "./components/Heading";
import Piano from "./components/Piano";
import Links from "./components/Links";
// import Instruction from "./components/Instruction";

export default {
  name: "App",
  components: { Heading, Piano, Links },
  methods: {},
};
</script>

<style>
.section {
  min-height: 100vh !important;
  background-color: #F4ECD8;
  color: #3D3D3D;
}
</style>
