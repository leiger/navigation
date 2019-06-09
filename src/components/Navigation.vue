<template>
  <v-card>
    <v-toolbar class="blue-grey" dark card dense>
      <v-toolbar-title class="subheading">{{cardTitle}}</v-toolbar-title>
    </v-toolbar>

    <v-card-text>
      <v-item-group v-for="(navList,i) in navLists" :key="i" multiple>
        <v-subheader>{{navList.tagName}}</v-subheader>
        <v-item v-for="nav in navList.websites" :key="nav.name">
          <v-btn @click="openSrc(nav.src)" depressed small>
            <span>{{nav.name}}</span>
          </v-btn>
        </v-item>
      </v-item-group>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Search extends Vue {
  cardTitle: string = "Navigation";
  navLists: { tagName: string; websites: { name: string; src: string }[] }[] = [
    {
      tagName: "Search Engine",
      websites: [
        {
          name: "google",
          src: "https://www.google.com/"
        },
        {
          name: "baidu",
          src: "https://www.baidu.com/"
        },
        {
          name: "zhihu",
          src: "https://www.zhihu.com/"
        }
      ]
    },
    {
      tagName: "Port",
      websites: [
        {
          name: ":8080",
          src: "localhost:8080"
        }
      ]
    },
    {
      tagName: "Vue",
      websites: [
        {
          name: "Vue.js",
          src: "https://vuejs.org/"
        },
        {
          name: "vue-router",
          src: "https://router.vuejs.org/"
        },
        {
          name: "vuex",
          src: "https://vuex.vuejs.org/"
        },
        {
          name: "element ui",
          src: "https://element.eleme.io/#/zh-CN/component/installation"
        },
        {
          name: "vuetify",
          src: "https://vuetifyjs.com/en/framework/colors"
        },
        {
          name: "iview",
          src: "https://www.iviewui.com/docs/guide/start"
        }
      ]
    },
    {
      tagName: "Front-end",
      websites: [
        {
          name: "mozilla",
          src: "https://developer.mozilla.org/en-US/"
        },
        {
          name: "react",
          src: "https://reactjs.org/"
        },
        {
          name: "sass",
          src: "https://sass-lang.com/guide"
        },
        {
          name: "less",
          src: "http://lesscss.org/usage/"
        }
      ]
    },
    {
      tagName: "Design",
      websites: [
        {
          name: "awwwards",
          src: "https://www.awwwards.com/"
        },
        {
          name: "iconfont",
          src: "https://www.iconfont.cn/"
        },
        {
          name: "material font",
          src: "https://material.io/tools/icons/?style=baseline"
        },
        {
          name: "google Fonts",
          src: "https://fonts.google.com/"
        }
      ]
    },
    {
      tagName: "Learn",
      websites: [
        {
          name: "codewithmosh",
          src: "https://codewithmosh.com/courses/enrolled"
        }
      ]
    },
    {
      tagName: "Entertainment",
      websites: [
        {
          name: "bilibili",
          src: "https://www.bilibili.com/"
        },
        {
          name: "netflix",
          src: "https://www.netflix.com/ca/"
        },
        {
          name: "douyu",
          src: "https://www.douyu.com/"
        },
        {
          name: "youtube",
          src: "https://www.youtube.com/"
        }
      ]
    }
  ];

  mounted() {
    if (localStorage.getItem("navLists")) {
      try {
        this.navLists = JSON.parse(localStorage.getItem("navLists")!);
      } catch (e) {
        localStorage.removeItem("navLists");
      }
    }
  }

  openSrc(url: string): void {
    window.location.href = url;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
