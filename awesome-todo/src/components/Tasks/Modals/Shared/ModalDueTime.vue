<template>
  <div class="q-mb-sm">
    <q-input
      outlined
      :value="dueTime"
      label="Due time"
      clearable
      @input="$emit('update:dueTime',$event)"
    >
      <template v-slot:append>
        <q-icon name="access_time" class="cursor-pointer">
          <q-popup-proxy transition-show="scale" transition-hide="scale">
            <q-time :value="dueTime" @input="$emit('update:dueTime', $event)" />
          </q-popup-proxy>
        </q-icon>
      </template>
    </q-input>
  </div>
</template>

<script>
export default {
  props: ["dueTime"],
};
</script>

<style>
</style>