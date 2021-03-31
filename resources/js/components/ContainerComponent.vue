<template>
  <div v-if="menu == 1">
    <!-- requisicion -->
      <requisicion-component></requisicion-component>
  </div>
</template>
<script>
export default {
  props: {
    menu: 0,
  },
};
</script>