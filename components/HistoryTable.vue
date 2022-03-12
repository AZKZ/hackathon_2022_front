<template>
  <div>
    <b-table
      sticky-header="500px"
      striped
      hover
      show-empty
      bordered
      :busy.sync="isBusy"
      :items="items"
      head-row-variant="success"
    >
    </b-table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";

@Component({
  name: "HistoryTable",
})
export default class HistoryTable extends Vue {
  @Prop({ type: Boolean, required: true })
  isBusy: any;

  @Prop({ type: Array, required: true })
  items: any;

  // fields = [
  //   { key: "paymentName", label: "料金種別" },
  //   { key: "useDate", label: "利用日" },
  //   { key: "storeId", label: "生年月日" },
  //   { key: "payment", label: "料金種別" },
  //   { key: "gender", label: "性別" },
  // ];
}
</script>
