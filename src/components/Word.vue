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

    const keys =
      this.wordSet[w].kana_keys[ws1] + this.wordSet[w].kana_keys[ws2];

    const latencyMs = 500;
    const targetKpm = 600;
    const timeout = latencyMs + (keys.length / targetKpm) * 60000;
    const intervalMs = 500;
    this.timer = setTimeout(() => {
      this.kana = "";
      this.roma = "";
      this.timer = setTimeout(this.updateWord, intervalMs);
    }, timeout);
  }

  mounted(): void {
    this.timer = setTimeout(this.updateWord, 0);
  }

  destroyed(): void {
    clearTimeout(this.timer);
  }
}
</script>

<style scoped>
.word {
  margin-top: 40vh;
  text-align: center;
  font-size: large;
  color: #eeeeee;
}
</style>
