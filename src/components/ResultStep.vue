<template>
  <div>
    <h1>Summary<br><small>{{formData.name }}</small></h1>
    <div class="text-gray-600 text-sm py-1">Name : {{ formData.name }}</div>
    <div class="text-gray-600 text-sm py-1">Age : {{ formData.age }}</div>
    <div class="text-gray-600 text-sm py-1">Where do you live : {{ formData.city.country }}</div>
    <div class="text-gray-600 text-sm py-1">Package : {{ formData.package.name }}</div>
    <div class="text-gray-600 text-sm py-1">
      Premium : {{ formData.premium }} {{ formData.city.currency }}
    </div>
    <div class="mt-6">
      <button class="button-white mr-2" @click="$emit('onBack')">Back</button>
      <button class="button-black ml-2">Buy</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ResultStep',
  props: {
    formData: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
</style>
