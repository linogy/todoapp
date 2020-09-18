<template>
  <div>
    <q-card-section class="row">
      <div class="text-h6">
        <slot></slot>
      </div>
      <q-space></q-space>
      <q-btn v-close-popup flat round dense icon="close"></q-btn>
    </q-card-section>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>