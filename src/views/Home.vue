<template>
  <div class="home">
    <MyTextarea :value="input" :readonly="false" @input="onInput" />
    <MyTextarea :value="translate(input)" :readonly="true" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"
import HelloWorld from "@/components/HelloWorld.vue"
import MyTextarea from "@/components/MyTextarea.vue"
import { cards } from "./cards.json"

@Component({
  components: {
    HelloWorld,
    MyTextarea
  }
})
export default class Home extends Vue {
  input = ""

  onInput(value: string) {
    this.input = value
  }

  translate(input: string): string {
    const words = input.split(",").map(w => w.trim())
    return words
      .map(w => {
        const card = cards.find(c => c.en === w)
        return card ? card.ja : w
      })
      .join(", ")
  }
}
</script>
