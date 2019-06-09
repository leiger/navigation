<template>
  <div class="clock">
    <v-card>
      <v-toolbar class="blue-grey" dark card dense>
        <v-icon>alarm</v-icon>
      </v-toolbar>
      <v-container>
        <div class="timer display-1 text-xs-center">
          <span class="d-block mb-2">{{`${min}:${sec}`}}</span>

          <v-btn v-if="clockState === 'start' " key="start" @click="start">Start</v-btn>
          <v-btn
            v-else-if="clockState === 'stop'"
            key="stop"
            outline
            color="red lighten-3"
            fab
            flat
            small
            @click="reset"
          >
            <v-icon>close</v-icon>
          </v-btn>
          <v-btn v-else key="finish" color="green" @click="reset" outline fab flat small>
            <v-icon>done</v-icon>
          </v-btn>
        </div>
      </v-container>
    </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Clock extends Vue {
  clockState: string = "start";
  min: string = "25";
  sec: string = "00";
  timer!: ReturnType<typeof setTimeout>;

  start(): void {
    this.clockState = "stop";
    let min = parseInt(this.min);
    let sec = parseInt(this.sec);

    this.timer = setInterval(() => {
      if (min > 0 || sec > 0) {
        if (sec === 0) {
          min--;
          sec = 60;
        }
        sec--;

        min < 10
          ? (this.min = "0" + min.toString())
          : (this.min = min.toString());

        sec < 10
          ? (this.sec = "0" + sec.toString())
          : (this.sec = sec.toString());
      } else {
        this.clockState = "finish";
        clearInterval(this.timer);
        let n = new Notification("Already 25 mins! Take a rest~", {
          dir: "auto",
          requireInteraction: true
        });
        console.log(n);
      }
    }, 1000);
  }

  reset(): void {
    clearInterval(this.timer);
    this.min = "25";
    this.sec = "00";
    this.clockState = "start";
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
