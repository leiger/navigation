<template>
  <div class="clipboar">
    <v-card>
      <v-toolbar class="blue-grey" dark card dense>
        <v-toolbar-title class="subheading">Clipboard</v-toolbar-title>
      </v-toolbar>
      <v-container>
        <v-textarea rows="10" color="" clearable name="" label="Clipboard 1"></v-textarea>
      </v-container>
    </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Clipboard extends Vue {
  // @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
