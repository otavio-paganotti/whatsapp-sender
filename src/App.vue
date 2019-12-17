<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
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
          Whatsapp Sender
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <zap />
    </q-page-container>
  </q-layout>
</template>

<script>
import zap from './components/zap.vue'

export default {
  name: 'LayoutDefault',

  components: {
    zap
  },

  data () {
    return {
      leftDrawerOpen: false
    }
  }
}
</script>

<style>
</style>
