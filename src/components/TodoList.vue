<template>
  <div class="todoList">
    <v-card>
      <v-toolbar class="blue-grey" dark card dense>
        <v-toolbar-title class="subheading">Todo List</v-toolbar-title>
        <v-spacer></v-spacer>

        <v-btn @click.stop="dialog = true" icon>
          <v-icon>add</v-icon>
        </v-btn>
        <v-btn @click.stop="openCalendar" icon>
          <v-icon>open_in_new</v-icon>
        </v-btn>
      </v-toolbar>

      <v-list dense subheader two-line>
        <v-subheader v-if="todos.length === 0">No Task.</v-subheader>
        <v-subheader v-else>
          <v-switch class="text-xs-right" v-model="filtered"></v-switch>
          <span v-if="!filtered">All tasks: {{computedTodos.length}}</span>
          <span v-else>Uncomplete tasks: {{computedTodos.length}}</span>
        </v-subheader>

        <div v-for="(todo, i) in computedTodos" :key="todo.time">
          <v-list-tile @click.stop="todo.done = !todo.done">
            <v-list-tile-action>
              <v-checkbox color="blue-grey darken-1" readonly v-model="todo.done"></v-checkbox>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title :class="{done: todo.done}">{{todo.title}}</v-list-tile-title>
            </v-list-tile-content>

            <v-list-tile-action>
              <v-list-tile-action-text>{{todo.time}}</v-list-tile-action-text>
              <v-btn icon flat color="red lighten-3" @click.stop="removeTodo(i)">
                <v-icon>close</v-icon>
              </v-btn>
            </v-list-tile-action>
          </v-list-tile>

          <v-divider v-if="i + 1 < todos.length" :key="`divider-${i}`"></v-divider>
        </div>
      </v-list>
    </v-card>

    <!-- dialog -->
    <v-layout row justify-center>
      <v-dialog max-width="380" v-model="dialog">
        <v-card>
          <v-card-title>
            <span>Add a Todo</span>
          </v-card-title>
          <v-card-text>
            <v-text-field autofocus v-model="newTodo" label="My Task" @keyup.enter="addTodo"></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat @click.prevent="dialog = false">Close</v-btn>
            <v-btn color="blue-grey darken-2" flat @click="addTodo">Save</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-layout>

    <!-- snackbar -->
    <v-snackbar v-model="snackbar.state" right top color="confirm">
      Confirm delete
      <v-btn flat icon @click="confirmRemoveTdo">
        <v-icon>done</v-icon>
      </v-btn>
      <v-btn flat icon @click="snackbar.state = false">
        <v-icon>close</v-icon>
      </v-btn>
    </v-snackbar>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class TodoList extends Vue {
  dialog: boolean = false;
  snackbar: { state: boolean; index: number } = { state: false, index: -1 };
  filtered: boolean = false;

  newTodo: string = "";
  todo: string[] = [];
  todos: { title: string; time: string; done: boolean }[] = [];

  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos")!);
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  }

  get computedTodos(): any {
    if (!this.filtered) return this.todos;
    return this.todos.filter(todo => todo.done === false);
  }

  addTodo(): void {
    var value = this.newTodo && this.newTodo.trim();
    if (!value) {
      return;
    }
    this.todos.unshift({
      title: this.newTodo,
      time: new Date().toLocaleTimeString(),
      done: false
    });
    // save to the localstorage
    this.saveTodos();

    // this.dialog = false;
    this.newTodo = "";
  }

  removeTodo(index: number): void {
    this.snackbar.state = true;
    this.snackbar.index = index;
  }

  confirmRemoveTdo(): void {
    this.todos.splice(this.snackbar.index, 1);
    this.saveTodos();
    this.snackbar.state = false;
  }

  saveTodos(): void {
    const parsed = JSON.stringify(this.todos);
    localStorage.setItem("todos", parsed);
  }

  openCalendar():void {
    window.location.href = 'https://calendar.google.com/calendar/r?tab=cc'
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.done {
  text-decoration: line-through;
  color: #bdbdbd;
}
</style>
