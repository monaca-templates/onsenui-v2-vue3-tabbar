<template>
  <v-ons-page>
    <v-ons-toolbar>
      <div class="center">{{ title }}</div>
    </v-ons-toolbar>

    <v-ons-tabbar
      position="auto"
      :tabs="tabs"
      :visible="true"
      v-model:active-index="activeIndex"
    >
    </v-ons-tabbar>
  </v-ons-page>
</template>

<script>
import { markRaw } from 'vue';
import settingsPage from "./Settings.vue";
import homePage from "./Home.vue";
import newsPage from "./News.vue";

export default {
  data() {
    return {
      activeIndex: 0,
      tabs: [
        {
          icon: this.md() ? null : "ion-ios-home",
          label: "Home",
          page: markRaw(homePage),
        },
        {
          icon: this.md() ? null : "ion-ios-notifications",
          label: "News",
          page: markRaw(newsPage),
          badge: 7,
        },
        {
          icon: this.md() ? null : "ion-ios-settings",
          label: "Settings",
          page: markRaw(settingsPage),
        },
      ],
    };
  },
  methods: {
    md() {
      return this.$ons.platform.isAndroid();
    },
  },
  computed: {
    title() {
      return this.tabs[this.activeIndex].label;
    },
  },
  components: { homePage, settingsPage, newsPage },
};
</script>
