<template>
  <div class="hello">
    <v-text-field :prepend-icon="icon" @click:prepend="changeSearchEngine" label="Search" append-icon="search" @click:append="handleSearch"></v-text-field>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Search extends Vue {
  // @Prop() private msg!: string;
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
