<template>
  <div>
    <b-input-group prepend="果物">
      <b-form-select v-model="_selected" :options="options"></b-form-select>
    </b-input-group>
  </div>
</template>

<script lang="ts">
import { Component, PropSync, Vue } from "nuxt-property-decorator";

@Component({
  name: "SampleSelect",
})
export default class SampleSelect extends Vue {
  @PropSync("selected", { type: String, required: true })
  _selected!: String;

  options = [
    { value: "apple", text: "リンゴ" },
    { value: "orange", text: "ミカン" },
    { value: "banana", text: "バナナ" },
  ];
}
</script>
