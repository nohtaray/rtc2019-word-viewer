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
  }[];

  private kana: string = "";
  private roma: string = "";
  private timer: number | undefined;

  private updateWord() {
    const w = Math.floor(Math.random() * 3);
    const ws1 = Math.floor(Math.random() * 100);
    const ws2 = Math.floor(Math.random() * 100 + 100);
    this.kana = this.wordSet[w].kanas[ws1] + this.wordSet[w].kanas[ws2];
    this.roma = this.wordSet[w].romas[ws1] + this.wordSet[w].romas[ws2];
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
