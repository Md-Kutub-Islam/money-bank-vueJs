<template>
  <q-layout view="hHh lpR lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          <div class="row colunm items-center absolute-center">
            <q-icon name="currency_rupee" />
            MoneyBanks
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      class="bg-primary text-white"
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      width="250"
      breakpoint="767"
    >
      <q-list>
        <q-item-label header class="text-white"> Navigation </q-item-label>

        <NavLink class="text-white" v-for="link in navList" :key="link.title" v-bind="link" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import NavLink from 'src/components/Nav/NavLink.vue'

const navList = [
  {
    title: 'Entries',
    icon: 'currency_rupee',
    link: '/',
  },
  {
    title: 'Settings',
    icon: 'settings',
    link: 'setting',
  },
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>
