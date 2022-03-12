<template>
  <div>
    <b-row class="mb-3">
      <h1>一覧画面</h1>
    </b-row>
    <b-row class="mb-3">
      <b-col sm="4">
        <b-input-group prepend="名前">
          <b-input v-model="inputForm.name" />
        </b-input-group>
      </b-col>
      <b-col sm="4">
        <SampleSelect :selected.sync="inputForm.paymentCode" />
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
      // alert("Error");

      // 暫定コード START
      var dummy = [
        {
          name: "田中 太郎",
          birthday: "1995-07-02",
          gender: "男性",
          payment: ["AAA", "BBBB"],
        },
      ];
      this.items.splice(0);
      this.items.push(...dummy);

      // 暫定コード END

      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };
}
</script>
