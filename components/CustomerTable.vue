<template>
  <div>
    <b-table
      sticky-header="500px"
      striped
      hover
      show-empty
      bordered
      fixed
      :busy.sync="isBusy"
      :fields="fields"
      :items="items"
      head-row-variant="success"
    >
      <template #cell(actions)="row">
        <b-button variant="info" @click="goHistory(row.item.id)">
          詳細
        </b-button>
        <b-button variant="info" @click="alert(row)"> 編集 </b-button>
      </template>
    </b-table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";

@Component({
  name: "CustomerTable",
})
export default class CustomerTable extends Vue {
  @Prop({ type: Boolean, required: true })
  isBusy = false;

  @Prop({ type: Array, required: true })
  items: any;

  fields = [
    { key: "actions", label: "", tdClass: "text-center" },
    { key: "name", label: "名前" },
    { key: "birthday", label: "生年月日" },
    { key: "paymentName", label: "料金種別" },
    { key: "gender", label: "性別" },
  ];

  goHistory(customerId: any) {
    this.$router.push({ path: `/history?customerId=${customerId}` });
  }
}
</script>
