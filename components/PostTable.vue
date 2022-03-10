<template>
  <div>
    <b-table striped hover :busy.sync="isBusy" :items="items"></b-table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

@Component({
  name: "PostTable",
})
export default class PostTable extends Vue {
  isBusy = false;
  items: any = [];

  mounted() {
    this.fetchPosts();
  }

  fetchPosts = async () => {
    this.isBusy = true;

    try {
      const response = await this.$axios.get(
        `https://jsonplaceholder.typicode.com/posts`
      );

      this.items.splice(0);
      Array.prototype.push.apply(this.items, response.data);
    } catch (error) {
      alert("Error");
      console.error(error);
    } finally {
      this.isBusy = false;
    }
  };
}
</script>
