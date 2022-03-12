<template>
  <div>
    <b-input-group prepend="料金種別">
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
  name: "PaymentSelect",
})
export default class PaymentSelec extends Vue {
  @PropSync("selected", { type: String, required: true })
  _selected!: String;

  @Prop({ type: Boolean, required: true })
  disabled: any;

  options = [
    { value: "1", text: "10回払い" },
    { value: "2", text: "20回払い" },
    { value: "3", text: "月会員" },
    { value: "4", text: "年会員" },
  ];
}
</script>
