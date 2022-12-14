<script>
export default {
  props: ["class", "type", "title", "style"],
};
</script>

<template>
  <button :class="class" :type="type" :style="style">{{ title }}</button>
</template>
