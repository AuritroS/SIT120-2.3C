<!-- 10. Components -->
<template>
  <div v-for="value in tests" :key="value.id">
    <p>{{ value.title }}</p>
    <p>{{ value.body }}</p>
    <p><slot /></p>
    <button @click="$emit('enlarge-text')">Enlarge Text</button>
  </div>
</template>

<script>
export default {
  props: ["tests"],
};
</script>
