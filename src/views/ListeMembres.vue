<script setup>
import { ref, onMounted, inject } from 'vue';
import { useMembresStore } from '@/stores/membres'

// const membresStore = inject('membres');
const membresStore = useMembresStore();


</script>

<template>
  <main>
    <h2 class="title">Liste des membres</h2>
    <ul>
      <router-link to="/profil-membre" class="">
        <li class="box" v-for="membre in membresStore.state.membres">
            <h2 class="title is-3">{{ membre.fullname }}</h2>
            <p class="subtitle">{{ membre.email }}</p>
        </li>
      </router-link>
    </ul>
  </main>
</template>
