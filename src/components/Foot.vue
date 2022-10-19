<template>
  <footer :style="`background-color: ${footerColor}`"></footer>
</template>

<script>
export default {
  name: "Foot",
  data() {
    return {
      footerColor: "slategrey",
    };
  },
};
</script>
