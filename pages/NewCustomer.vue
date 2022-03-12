<template>
  <div>
    <b-row class="mb-3">
      <h1>顧客登録画面</h1>
    </b-row>
    <b-row class="mb-3">
      <b-col>
        <b-input-group prepend="名前">
          <b-input v-model="inputForm.name" />
        </b-input-group>
      </b-col>
    </b-row>
    <b-row class="mb-3">
      <b-col>
        <b-input-group prepend="生年月日">
          <b-form-datepicker v-model="inputForm.birthday" />
        </b-input-group>
      </b-col>
    </b-row>
    <b-row class="mb-3">
      <b-col>
        <PaymentSelect :selected.sync="inputForm.paymentCode" />
      </b-col>
    </b-row>
    <b-row class="mb-3">
      <b-col>
        <GenderSelect :selected.sync="inputForm.gender" />
      </b-col>
    </b-row>
    <b-row class="mb-3">
      <b-col>
        <b-button variant="info" @click="register">登録</b-button>
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
    paymentCode: "",
    birthday: "",
    gender: "",
  };
  alertObj = {
    dismissCountDown: 0,
  };

  register = async () => {
    this.isBusy = true;

    // 未入力の場合はアラートを表示する。
    if (
      !this.inputForm.name ||
      !this.inputForm.paymentCode ||
      !this.inputForm.birthday ||
      !this.inputForm.gender
    ) {
      alert("未入力項目があります。");
      return;
    }

    try {
      const res = await this.$axios.post(
        `http://localhost:8080/customers/`,
        this.inputForm
      );

      alert("登録が完了しました。");
      this.$router.push({ path: "/search" });
    } catch (error) {
      // 暫定コード START
      alert("登録が完了しました。");
      this.$router.push({ path: "/search" });
      // 暫定コード END

      alert("Error");
      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };
}
</script>
