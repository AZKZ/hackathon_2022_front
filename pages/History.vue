<template>
  <div>
    <b-row class="mb-3">
      <h2>詳細画面</h2>
    </b-row>
    <b-row class="mb-3">
      <b-col sm="3">
        <b-input-group prepend="名前">
          <b-input v-model="customer.name" disabled />
        </b-input-group>
      </b-col>
      <b-col sm="3">
        <b-input-group prepend="生年月日">
          <b-input v-model="customer.birthday" disabled />
        </b-input-group>
      </b-col>
      <b-col sm="3">
        <b-input-group prepend="性別">
          <b-input v-model="customer.gender" disabled />
        </b-input-group>
      </b-col>
    </b-row>

    <HistoryTable :items="items" :isBusy="isBusy" />
    <b-row class="mb-3">
      <b-col>
        <b-button variant="info" @click="back">戻る</b-button>
      </b-col>
    </b-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

@Component({
  name: "History",
})
export default class History extends Vue {
  isBusy = false;
  items: any = [];
  customer = {
    name: "",
    birthday: "",
    gender: "",
  };

  mounted() {
    this.fetchCustomer();
  }

  fetchCustomer = async () => {
    this.isBusy = true;
    const customerId = this.$route.query.customerId;

    if (!customerId) {
      alert("顧客IDがありません。");
      this.$router.push({ path: "/search" });
      return;
    }

    try {
      const res = await this.$axios.get(
        `/api/history?customerId=${customerId}`
      );

      this.customer.name = res.data.name;
      this.customer.birthday = res.data.birthday;
      this.customer.gender = res.data.gender;

      this.items.splice(0);
      this.items.push(...res.data.histories);
    } catch (error) {
      alert("Error");
      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };

  back() {
    this.$router.push({ path: "/search" });
  }
}
</script>
