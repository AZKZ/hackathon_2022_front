<template>
  <div>
    <b-input-group prepend="性別">
      <b-form-select
        v-model="_selected"
        :options="options"
        :disabled="disabled"
      ></b-form-select>
    </b-input-group>
  </div>
</template>

<script lang="ts">
import { Component, Prop, PropSync, Vue } from "nuxt-property-decorator";

@Component({
  name: "GenderSelect",
})
export default class GenderSelect extends Vue {
  @PropSync("selected", { type: String, required: true })
  _selected!: String;

  @Prop({ type: Boolean, required: true })
  disabled: any;

  options = [
    { value: "0", text: "男性" },
    { value: "1", text: "女性" },
  ];
}
</script>
