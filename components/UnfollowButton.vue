<template>
  <b-button variant="danger"
            class="mr-2"
            @click="unfollow"
  >
    <font-awesome-icon icon="spinner"
                       spin
                       v-if="isLoading"
    />
    <span v-else>unfollow</span>
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
  props: ['isLoading', 'unfollow']
};
</script>

<style scoped>
</style>
