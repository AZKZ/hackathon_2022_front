<template>
  <div>
    <b-table
      sticky-header="500px"
      striped
      hover
      bordered
      :busy.sync="isBusy"
      :items="items"
      head-row-variant="success"
    ></b-table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";

@Component({
  name: "PostTable",
})
export default class PostTable extends Vue {
  @Prop({ type: Boolean, required: true })
  isBusy = false;

  @Prop({ type: Array, required: true })
  items: any;
}
</script>
