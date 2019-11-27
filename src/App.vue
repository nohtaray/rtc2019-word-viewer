<template>
  <v-app>
    <v-content>
      <Word :word-set="[rtcWords.computer, rtcWords.sports, rtcWords.heisei]" />
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import Word from "./components/Word.vue";
import rtcWords from "./assets/rtc2019words.json";

export default Vue.extend({
  name: "App",

  components: {
    Word
  },

  data: () => ({
    rtcWords
  })
});
</script>

<style>
v-content {
  background-color: black;
}
</style>
