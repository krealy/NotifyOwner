<template>
  <div>
    <NotifyOwner />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import NotifyOwner from './components/NotifyOwner.vue';

export default defineComponent({
  components: {
    NotifyOwner
  }
});
</script>
