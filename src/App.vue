<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="glossy" style="background-color: #5ab76a;">
      <q-toolbar>
        <!-- <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
          icon="menu"
        /> -->

        <q-toolbar-title>
          Erural
        </q-toolbar-title>

        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>   

    <q-page-container>
      <Home />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue'
import Home from './components/Home.vue'

export default {
  name: 'LayoutDefault',

  components: {
    Home
  },

  setup () {
    return {
      leftDrawerOpen: ref(false)
    }
  }
}
</script>
