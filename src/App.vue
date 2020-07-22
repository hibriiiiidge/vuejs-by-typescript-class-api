<template>
  <div id="app">
    <p>{{ greetText }}</p>
    <p>挨拶した回数 : {{ count }}回</p>
    <p v-if="isRegulars">いつもありがとうございます</p>
    <p>
      <MyButton :greet="greetText" @click="onMyButtonClicked" class="my-button">
        挨拶する
      </MyButton>
    </p>
    <p>
      <ResetButton v-model="greetText" />
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Watch, Vue } from "vue-property-decorator";
import MyButton from "@/components/MyButton.vue";
import ResetButton from "@/components/ResetButton.vue";

@Component({
  components: {
    MyButton,
    ResetButton
  }
})
export default class App extends Vue {
  private count = 0;
  public greetText = "hello!!";

  public get isRegulars(): boolean {
    return this.count >= 5;
  }

  @Watch('count')
  public countChanged() {
    if (this.count === 5) {
      alert("常連になりました");
    }
  }

  public onMyButtonClicked(count: number) {
    this.count = count;
    this.greetText = "こんにちは";
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
