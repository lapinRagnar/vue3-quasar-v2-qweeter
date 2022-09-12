<template>
  <q-layout view="lHr lpR fFf">

    <q-header bordered class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold">
          Mon super qwitter
        </q-toolbar-title>

        <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
      </q-toolbar>
    </q-header>

    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      bordered
      :width="200"
    >

      <q-icon
        class="q-pa-md"
        name="fa-solid fa-earth-americas"
        size="lg"
        color="primary"
      />


      <q-list >

        <q-item
          clickable
          v-ripple
          to="/"
          >
          <q-item-section avatar>
            <q-icon
              name="house"
              size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">Accueil</q-item-section>
        </q-item>

        <q-item
          clickable
          v-ripple
          to="/about"
          >
          <q-item-section avatar>
            <q-icon
              name="info"
              size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">about</q-item-section>

        </q-item>


      </q-list>


    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    }
  }
}
</script>
