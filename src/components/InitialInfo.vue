<template>
  <div class="hello">
    <img alt="Vue logo" src="./../assets/drawing.svg">
    <h1>Welcome to VLAVAAV!</h1>
    <p>
      VLAVAAV is a no-nonsense color palette vizualization tool.
      Just paste your color codes to the browser to see them!
    </p>
    <p>
      Try these colors out:
      <pre>{{ sample_palette }}</pre>
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class InitialInfo extends Vue {
  private sample_palette = [
    '#FF0000',
    '#00FF00',
    '#0000FF',
  ].join('\n');
}
</script>

<style scoped lang="scss">
</style>