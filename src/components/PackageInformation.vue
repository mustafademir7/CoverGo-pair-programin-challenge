<template>
  <small>
     (+{{ difference }} {{ currencyType }} {{ packageInfo.val }} %)
  </small>
</template>

<script>
export default {
  name: 'PackageInformation',
  props: {
    packageInfo: {
      type: Object,
      required: true,
    },
    city: {
      type: Object,
      default: () => {},
    },
    age: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    currencyType() {
      return this.city.currency;
    },
    difference() {
      const rate = this.city.rate ?? 1;
      const age = this.age ?? 0;
      const percent = this.packageInfo.val ?? 0;
      const total = age * 10 * rate;
      if (percent) {
        return (total * percent) / 100;
      }
      return 0;
    },
  },
};
</script>

<style scoped>

</style>
