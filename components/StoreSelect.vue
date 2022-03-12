<template>
  <div>
    <b-input-group prepend="店舗">
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
  name: "StoreSelect",
})
export default class StoreSelect extends Vue {
  @PropSync("selected", { type: String, required: true })
  _selected!: String;

  @Prop({ type: Boolean, required: true })
  disabled: any;

  options = [
    { value: "1", text: "新宿" },
    { value: "2", text: "渋谷" },
  ];
}
</script>
