<template>
  <div class="word">
    <div class="kana">{{ kana }}</div>
    <div class="roma">{{ roma }}</div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Word extends Vue {
  @Prop() private wordSet!: {
    kana_keys: string[];
    kanas: string[];
    romas: string[];
  };

  private kana: string = "";
  private roma: string = "";
  private timer: number | undefined;

  private updateWord() {
    const size = this.wordSet.kanas.length;
    const w1 = Math.floor((Math.random() * size) / 2);
    const w2 = Math.floor((Math.random() * size) / 2 + size / 2);
    this.kana = this.wordSet.kanas[w1] + this.wordSet.kanas[w2];
    this.roma = this.wordSet.romas[w1] + this.wordSet.romas[w2];
  }

  mounted(): void {
    this.timer = setInterval(this.updateWord, 3000);
  }
  destroyed(): void {
    clearInterval(this.timer);
  }
}
</script>

<style scoped></style>
