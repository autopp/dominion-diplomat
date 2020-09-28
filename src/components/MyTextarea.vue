<template>
  <textarea
    rows="3"
    cols="50"
    :readonly="readonly"
    :placeholder="placeholder"
    :value="value"
    @input="onInput($event.target.value)"
  >
  </textarea>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator"

@Component
export default class MyTextarea extends Vue {
  @Prop() private value!: string
  @Prop() private placeholder!: string
  @Prop() private readonly!: boolean

  onInput(value: string) {
    this.$emit("input", value)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
