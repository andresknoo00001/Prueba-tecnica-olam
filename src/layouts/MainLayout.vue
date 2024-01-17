<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="bg-red">
        <q-toolbar-title class="text-center">
          Prueba tecnica olma (responsive app)</q-toolbar-title
        >
      </q-toolbar>
    </q-header>
    <q-page-container class="row items-start justify-center q-pa-md">
      <getLetters></getLetters>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";
import getLetters from "../components/GetLetters.vue";

const linksList = [
  {
    title: "Input info",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: { getLetters },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
