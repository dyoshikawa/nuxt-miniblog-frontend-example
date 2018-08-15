<template>
  <b-button variant="info"
            class="mt-2 mb-2"
  >
    <font-awesome-icon :icon="iconName"
                      color="white"
                      class="arrow-button"
    />
  </b-button>
</template>

<script>
import { library, config } from '@fortawesome/fontawesome-svg-core';
import {
  faArrowAltCircleLeft,
  faArrowAltCircleRight
} from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

config.autoAddCss = false;
library.add(faArrowAltCircleLeft, faArrowAltCircleRight);

export default {
  components: {
    FontAwesomeIcon
  },
  props: ['direction'],
  data() {
    return {
      iconName: ''
    };
  },
  created() {
    if (this.direction === 'left') {
      this.iconName = 'arrow-alt-circle-left';
    } else if (this.direction === 'right') {
      this.iconName = 'arrow-alt-circle-right';
    }
  }
};
</script>

<style scoped>
.arrow-button {
  width: 50px;
  text-align: right;
}
</style>
