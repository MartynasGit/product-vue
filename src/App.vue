<template>
  <div>
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <nav class="bg-gray-400">
        <router-link to="/">Home</router-link>
        <router-link to="/feed">Uzsakymai</router-link>
        <router-link to="/register">Registruotis</router-link>
        <router-link to="/sign-in">Prisijungti</router-link>
        <button @click="handleSignOut" v-if="isLoggedIn">Atsijungti</button>
      </nav>
      <router-view />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { getAuth, onAuthStateChanged, signOut } from 'firebase/auth';
import router from './Router';

const isLoggedIn = ref(false);

let auth;

onMounted(() => {
  auth = getAuth();
  onAuthStateChanged(auth, (user) => {
    if (user) {
      isLoggedIn.value = true;
    }
    else {
      isLoggedIn.value = false;
    }
  })
})

const handleSignOut = () => {
  signOut(auth).then(() => {
    router.push("/");
  })
}

</script>