<template>
  <b-button variant="success"
            class="mr-2"
            @click="follow"
  >
    <font-awesome-icon icon="spinner"
                       spin
                       v-if="isLoading"
    />
    <span v-else>follow</span>
  </b-button>
</template>

<script lang="ts">
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

library.add(faSpinner);

export default {
  components: {
    FontAwesomeIcon
  },
  props: ['isLoading', 'follow']
};
</script>

<style scoped>
</style>
