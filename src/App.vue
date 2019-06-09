<template>
  <div id="app">
    <v-app>
      <v-content>
        <v-container class="container-box" fluid grid-list-md>
          <v-layout row wrap fill-height>
            <v-flex d-flex sm12 md8>
              <v-layout column fill-height>
                <v-flex d-flex sm12 md3>
                  <v-card color="blue" dark>
                    <v-card-text>{{ lorem.slice(0, 70) }}</v-card-text>
                  </v-card>
                </v-flex>
                <v-flex d-flex sm12 md9>
                  <v-card color="indigo" dark>
                    <v-card-text>{{ lorem.slice(0, 70) }}</v-card-text>
                  </v-card>
                </v-flex>
              </v-layout>
            </v-flex>
            <v-flex d-flex sm12 md4>
              <v-layout column>
                <v-flex d-flex sm12 md6>
                  <TodoList></TodoList>
                </v-flex>
                <v-flex d-flex sm12 md6>
                  <v-card color="red" dark>
                    <v-card-text>{{ lorem.slice(0, 70) }}</v-card-text>
                  </v-card>
                </v-flex>
              </v-layout>
            </v-flex>
          </v-layout>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import TodoList from "./components/TodoList.vue";

@Component({
  components: {
    TodoList
  }
})
export default class App extends Vue {
  lorem: string = `Lorem ipsum dolor sit amet, mel at clita quando. Te sit oratio vituperatoribus, nam ad ipsum posidonium mediocritatem, explicari dissentiunt cu mea. Repudiare disputationi vim in, mollis iriure nec cu, alienum argumentum ius ad. Pri eu justo aeque torquatos.`;
}
</script>

<style lang="scss">
#app {
  .container-box {
    height: 100vh;
  }
}
</style>
