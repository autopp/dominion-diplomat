<template>
  <div class="container">
    <div class="form-check">
      <input
        type="checkbox"
        class="form-check-input"
        id="showHeirloom"
        v-model="showHeirloom"
      />
      <label class="form-check-label" for="showHeirloom">家宝の表示</label>
    </div>
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
  showHeirloom = true

  onInput(value: string) {
    this.input = value
  }

  translate(input: string): string {
    const words = input.split(",").map(w => w.trim())
    return words
      .map(w => {
        const card = cards.find(c => c.en === w)

        if (!card) {
          return w
        }
        return this.showHeirloom && card.heirloom
          ? `${card.ja}/${card.heirloom}`
          : card.ja
      })
      .join(", ")
  }
}
</script>
