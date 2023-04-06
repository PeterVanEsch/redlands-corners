<template>
  <div class="home">
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
})
export default class Home extends Vue {
  private allStreets = ['1st', 'Gavin', 'Maple'];
  private street1 = '';
  private street2 = '';

  getDate() {
    return new Date();
  }

  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000);
    return day;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
