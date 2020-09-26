<template>
  <div class="home">
    <MyTextarea :value="input" :readonly="false" @input="onInput" />
    <MyTextarea :value="input" :readonly="true" @input="onInput" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"
import HelloWorld from "@/components/HelloWorld.vue"
import MyTextarea from "@/components/MyTextarea.vue"

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
}
</script>
