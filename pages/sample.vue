<template>
  <div>
    <b-table striped hover :items="items"></b-table>
    <!-- aaa -->
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

@Component({
  name: "Sample",
})
export default class Sample extends Vue {
  items = [
    { age: 40, first_name: "Dickerson", last_name: "Macdonald" },
    { age: 21, first_name: "Larsen", last_name: "Shaw" },
    { age: 89, first_name: "Geneva", last_name: "Wilson" },
    { age: 38, first_name: "Jami", last_name: "Carney" },
  ];
}
</script>
