<template>
  <div>
    <Navbar />
    <v-main class="ma-4">
      <slot />
    </v-main>
  </div>
</template>

<script>
import Navbar from "../../components/Navbar";
export default {
  components: { Navbar }
};
</script>

<style>
</style>