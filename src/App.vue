<template>
  <div id="app" @paste="onAppPaste">
    <template v-if="showInitialInfo">
      <InitialInfo v-if="showInitialInfo"/>
    </template>
    <ShowColors
      v-else
      :colors="colors"
    />
    <p v-if="errorMessageToShow">
      {{ errorMessageToShow }}
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import InitialInfo from '@/components/InitialInfo.vue';
import ShowColors from '@/components/ShowColors.vue';

@Component({
  components: {
    InitialInfo,
    ShowColors,
  },
})
export default class App extends Vue {
  private colors: string[] = [];

  private errorMessageToShow = '';

  public onAppPaste(pastedContent: ClipboardEvent) {
    let str = '';

    if (pastedContent.clipboardData) {
      str = pastedContent.clipboardData.getData('text');
      this.errorMessageToShow = '';
    } else {
      this.errorMessageToShow = 'Clipboard is empty, nothing was pasted!';
    }

    this.colors = this.findColors(str);
    if (!this.colors.length) this.errorMessageToShow = 'No colors of the #RRGGBB format were found in the pasted text.';
  }

  public findColors(pastedText: string): string[] {
    const colors = pastedText.match(/#[0-9a-fA-F]{6}/g) || [];
    return [...new Set(
      colors.map(color => color.toLowerCase()),
    )];
  }

  get showInitialInfo() {
    return !this.colors.length;
  }
}
</script>

<style lang="scss">
#app {
  align-items: center;
  background-color: #181818;
  color: #ffffff;
  display: flex;
  flex-direction: column;
  font-family: Helvetica, Arial, sans-serif;
  justify-content: center;
  min-height: 100vh;
  text-align: center;
}
</style>
