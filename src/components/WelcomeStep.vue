<template>
  <div class="welcome">
    <h1>Hello There!</h1>
    <div class="info">Let's buy some insurance It's going to take only a few steps</div>
    <button class="button-black" @click="$emit('onNext')">Start</button>
  </div>
</template>

<script>
export default {
  name: 'Welcome-wizard',
};
</script>

<style scoped>
  .info {
    @apply pt-8 pb-3;
  }
</style>
