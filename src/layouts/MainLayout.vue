<template>

  <q-layout view="lHr lpR fFf">

    <q-header bordered class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold">

          <span class="gt-sm">{{ $route.name }}</span>

          <q-icon
            class="q-pa-md lt-sm header-icon"
            name="fa-solid fa-earth-americas"
            size="sm"
            color="orange"
          />

        </q-toolbar-title>

        <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
      </q-toolbar>
    </q-header>


    <!-- menu à gauche -->
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
          exact
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
          exact
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

    <!-- menu à droite -->
    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>

      <q-input
        color="purple-12"
        v-model="text"
        label="recherche"
        class="q-ma-md"
        placeholder="rechercher qwitter..."
        dense
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>



      <q-list
        separator
      >

        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">OVERLINE</q-item-label>
            <q-item-label class="text-weight-bold">Single line item</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>


        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">OVERLINE</q-item-label>
            <q-item-label class="text-weight-bold">Single line item</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>


        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">OVERLINE</q-item-label>
            <q-item-label class="text-weight-bold">Single line item</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>




      </q-list>


    </q-drawer>


    <!-- la page centrale -->
    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
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

<style lang="scss">
  .header-icon{
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%)
  }
</style>
