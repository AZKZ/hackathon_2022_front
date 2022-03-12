<template>
  <div>
    <b-row>
      <b-col sm="6">
        <b-alert
          :show="alertObj.dismissCountDown"
          dismissible
          variant="success"
          @dismissed="alertObj.dismissCountDown = 0"
          @dismiss-count-down="countDownChanged"
        >
          登録が完了しました。
        </b-alert>
      </b-col>
    </b-row>

    <PostTable :items="items" :isBusy="isBusy" />

    <b-row>
      <b-col sm="4">
        <b-input-group prepend="XXX">
          <b-input v-model="inputForm.value" />
        </b-input-group>
      </b-col>
      <b-col sm="3">
        <b-button variant="info" @click="submitPost">SUBMIT</b-button>
      </b-col>
      {{ inputForm }}
    </b-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

interface Form {
  value: string;
}

@Component({
  name: "Sample",
})
export default class Sample extends Vue {
  isBusy = false;
  items: any = [];
  inputForm: Form = { value: "" };
  alertObj = {
    dismissCountDown: 0,
  };

  mounted() {
    this.fetchPosts();
  }

  fetchPosts = async () => {
    this.isBusy = true;

    try {
      const res = await this.$axios.get(
        "https://jsonplaceholder.typicode.com/posts"
      );

      this.items.splice(0);
      this.items.push(...res.data);
    } catch (error) {
      alert("Error");
      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };

  submitPost = async () => {
    try {
      const res = await this.$axios.post(
        "https://jsonplaceholder.typicode.com/posts",
        this.inputForm
      );

      this.alertObj.dismissCountDown = 2;

      console.log(res.data);
    } catch (error) {
      alert("Error");
      console.error(error);
    }
  };

  countDownChanged(dismissCountDown: number) {
    this.alertObj.dismissCountDown = dismissCountDown;
  }
}
</script>
