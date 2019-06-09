<template>
  <div id="app">
    <v-app>
      <v-content>
        <v-container class="container-box" fluid grid-list-md>
          <v-layout row wrap>
            <v-flex sm12 md5>
              <v-layout column>
                <v-flex>
                  <Navigation></Navigation>
                </v-flex>
              </v-layout>
            </v-flex>
            <v-flex sm12 md3>
              <v-layout column>
                <v-flex>
                  <Clipboard></Clipboard>
                </v-flex>
                <v-flex>
                  <Clock></Clock>
                </v-flex>
              </v-layout>
            </v-flex>
            <v-flex sm12 md4>
              <v-layout column>
                <v-flex>
                  <TodoList></TodoList>
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
import Search from "./components/Search.vue";
import Clipboard from "./components/Clipboard.vue";
import Navigation from "./components/Navigation.vue";
import Clock from "./components/Clock.vue";

@Component({
  components: {
    TodoList,
    Search,
    Clipboard,
    Navigation,
    Clock
  }
})
export default class App extends Vue {
  mounted() {
    if (!("Notification" in window)) {
      alert("This browser does not support desktop notification");
    }
    // Otherwise, we need to ask the user for permission
    else if (Notification.permission !== "denied") {
      Notification.requestPermission();
    }
  }
}
</script>

<style lang="scss">
#app {
}
</style>
