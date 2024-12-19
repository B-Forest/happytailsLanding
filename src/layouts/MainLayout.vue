<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="q-m-none">
      <q-toolbar class="toolbar">
        <img src="icons/happytails.png" alt="Logo" class="q-mr-sm" style="height: 40px" />
        <q-toolbar-title class="q-m-none">Happy Tails</q-toolbar-title>
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts"></script>

<style lang="scss">
.toolbar {
  padding-left: 2rem;
  background-color: $primary-second;
}
</style>
