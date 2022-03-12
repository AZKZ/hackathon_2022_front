<template>
  <div>
    <b-row class="mb-3">
      <h2>一覧画面</h2>
    </b-row>
    <b-row class="mb-3">
      <b-col sm="4">
        <b-input-group prepend="名前">
          <b-input v-model="inputForm.name" />
        </b-input-group>
      </b-col>
      <b-col sm="4">
        <PaymentSelect :selected.sync="inputForm.paymentCode" />
      </b-col>
    </b-row>
    <b-row class="mb-3">
      <b-col sm="5">
        <b-input-group prepend="生年月日_From">
          <b-form-datepicker v-model="inputForm.birthdayFrom" />
        </b-input-group>
      </b-col>
      <b-col sm="5">
        <b-input-group prepend="生年月日_To">
          <b-form-datepicker v-model="inputForm.birthdayTo" />
        </b-input-group>
      </b-col>
      <b-col>
        <b-button variant="info" @click="search">検索</b-button>
      </b-col>
    </b-row>
    <CustomerTable :items="items" :isBusy="isBusy" />
    <b-row class="mb-3">
      <b-col>
        <b-button variant="success" @click="goRegister">登録画面</b-button>
      </b-col>
    </b-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

@Component({
  name: "Search",
})
export default class Sample extends Vue {
  isBusy = false;
  items: any = [];
  inputForm = {
    name: "",
    selected: "",
    birthdayTo: "",
    birthdayFrom: "",
    paymentCode: "",
  };

  mounted() {
    // this.fetchPosts();
  }

  search = async () => {
    this.isBusy = true;
    console.log(this.inputForm);
    var queryParam = "";

    if (this.inputForm.name) {
      queryParam += `&name=${this.inputForm.name}`;
    }

    if (this.inputForm.paymentCode) {
      queryParam += `&paymentCode=${this.inputForm.paymentCode}`;
    }

    if (this.inputForm.birthdayFrom) {
      queryParam += `&birthdayFrom=${this.inputForm.birthdayFrom}`;
    }

    if (this.inputForm.birthdayTo) {
      queryParam += `&birthdayTo=${this.inputForm.birthdayTo}`;
    }

    try {
      const res = await this.$axios.get(`/api/customers/?${queryParam}`);

      this.items.splice(0);
      this.items.push(...res.data);
    } catch (error) {
      alert("Error");

      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };

  goRegister() {
    this.$router.push({ path: "newcustomer" });
  }
}
</script>
