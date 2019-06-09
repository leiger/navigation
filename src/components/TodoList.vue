<template>
  <div class="hello">
    <v-card>
      <v-toolbar class="blue-grey darken-1" dark card>
        <v-toolbar-title>Todo List</v-toolbar-title>
        <v-spacer></v-spacer>

        <v-btn @click.stop="dialog = true" icon>
          <v-icon>add</v-icon>
        </v-btn>
      </v-toolbar>

      <v-list subheader two-line>
        <v-subheader v-if="todos.length === 0">No Task.</v-subheader>
        <v-subheader v-else>
          
          <v-switch class="text-xs-right" v-model="filter"></v-switch>All Task.
        </v-subheader>

        <div v-for="(todo, i) in todos" :key="i">
          <v-list-tile ripple @click.prevent="toggleTodoDone(i)">
            <v-list-tile-action>
              <v-checkbox color="blue-grey darken-1" readonly v-model="todo.done"></v-checkbox>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title :class="{done: todo.done}">{{todo.title}}</v-list-tile-title>
            </v-list-tile-content>

            <v-list-tile-action>
              <v-list-tile-action-text>{{time}}</v-list-tile-action-text>
              <v-btn icon flat color="red lighten-3" @click="removeTodo(i)">
                <v-icon>close</v-icon>
              </v-btn>
            </v-list-tile-action>
          </v-list-tile>

          <v-divider v-if="i + 1 < todos.length" :key="`divider-${i}`"></v-divider>
        </div>
      </v-list>
    </v-card>

    <v-layout row justify-center>
      <v-dialog max-width="380" v-model="dialog">
        <v-card>
          <v-card-title>
            <span>Add a Todo</span>
          </v-card-title>
          <v-card-text>
            <v-text-field v-model="newTodo" label="My Task"></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat @click="dialog = false">Close</v-btn>
            <v-btn color="blue-grey darken-2" flat @click="addTodo">Save</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-layout>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  dialog: boolean = false;
  filter: boolean = false;
  newTodo: string = "";
  todo: string[] = [];
  todos: { title: string; done: boolean }[] = [];
  time: string = new Date().toLocaleTimeString();

  addTodo(): void {
    var value = this.newTodo && this.newTodo.trim();
    if (!value) {
      return;
    }
    this.todos.push({
      title: this.newTodo,
      done: false
    });
    this.dialog = false;
    this.newTodo = "";
  }

  toggleTodoDone(i: number): void {
    this.todos[i].done = !this.todos[i].done;
  }

  removeTodo(index: number): void {
    this.todos.splice(index, 1);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.done {
  text-decoration: line-through;
  color: #ccc;
}
</style>
