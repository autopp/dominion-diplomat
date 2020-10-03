<template>
  <div class="container">
    <div>
      <MyTextarea
        :value="input"
        placeholder="Smithy, Remodel"
        :readonly="false"
        @input="onInput"
      />
    </div>
    <div>
      <MyTextarea
        :value="translate(input)"
        placeholder="鍛冶屋, 改築"
        :readonly="true"
      />
    </div>
    <div>
      <button class="btn btn-primary" v-clipboard:copy="translate(input)">
        copy
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"
import MyTextarea from "@/components/MyTextarea.vue"
import { cards } from "./cards.json"

@Component({
  components: {
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
