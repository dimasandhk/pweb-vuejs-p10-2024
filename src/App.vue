<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <nav class="bg-gray-800 p-4">
    <div class="container mx-auto flex justify-between items-center">
      <div class="flex items-center space-x-4">
        <h3 class="text-white font-bold">Book App PWEB A | P10 🗿</h3>
      </div>
      <div class="hidden md:flex items-center space-x-4">
        <RouterLink to="/" class="text-white">Home</RouterLink>
        <RouterLink to="/add-book" class="text-white">Add New Book</RouterLink>
      </div>
    </div>
  </nav>

  <RouterView />
</template>
