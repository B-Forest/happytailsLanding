<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="q-m-none">
      <q-toolbar class="toolbar">
        <img src="icons/happytails.png" alt="Logo" class="q-mr-sm" style="height: 40px" />
        <q-toolbar-title class="q-m-none">Happy Tails</q-toolbar-title>
        <q-space />
        <a
          href="https://www.figma.com/proto/9Q4ueceD5IAdSOJTx1cErs/Happy-Tails?node-id=62-320&t=WD2fsBVslkesIUWp-1&scaling=scale-down&content-scaling=fixed&page-id=1%3A3&starting-point-node-id=62%3A320"
          target="_blank"
          class="demo-link"
          >Testez notre démo</a
        >
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

.demo-link {
  display: inline-block;
  background-color: #ff9a76;
  color: white;
  text-decoration: none;
  font-weight: bold;
  padding: 10px 20px;
  border-radius: 25px;
  transition:
    background-color 0.3s,
    transform 0.2s;
  font-family: Arial, sans-serif;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.demo-link:hover {
  background-color: #ff7f5e; /* Slightly darker shade for hover */
  transform: translateY(-2px); /* Lift effect on hover */
}

.demo-link:active {
  transform: translateY(1px); /* Subtle press effect */
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
}
</style>
