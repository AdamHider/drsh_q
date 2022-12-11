<template>
  <AppBackground/>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <router-view />
    </q-page-container>
    <q-footer bordered class="bg-grey-8 text-white">
      <q-tabs v-if="bottomBar">
          <q-route-tab
              icon="home"
              to="/home"
              exact
          />
          <q-route-tab
              icon="classroom"
              to="/classroom"
              exact
          />
          <q-route-tab
              icon="notifications"
              to="/notifications"
              exact
          />
          <q-route-tab
              icon="alarm"
              to="/user-dashboard"
              exact
          />
      </q-tabs>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref, watch } from 'vue'
import AppBackground from 'components/AppBackground.vue'
import { useRoute } from "vue-router";

const route = useRoute();

const bottomBar = ref(true);
  if(route.meta.noBottomBar){
    bottomBar.value = false;
  }

watch(route, (currentValue, oldValue) => {
  console.log(currentValue.meta);
  if(currentValue.meta.noBottomBar){
    bottomBar.value = false;
  } else {
    bottomBar.value = true;
  }
});
</script>
