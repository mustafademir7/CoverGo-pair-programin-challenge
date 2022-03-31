<template>
  <div class="wizard-container">
      <component :is="components[step]"
                 @onNext="onNextHandler"
                 @onBack="step--"
                 @onReset="step = 0"
                 :formData="formData" />
  </div>
</template>

<script>
const WelcomeStep = () => import('@/components/WelcomeStep.vue');
const FormStep = () => import('@/components/FormStep.vue');
const ResultStep = () => import('@/components/ResultStep.vue');

export default {
  name: 'HomeView',
  data() {
    return {
      step: 0,
      components: [WelcomeStep, FormStep, ResultStep],
      formData: {
        name: '',
        age: 0,
        city: {},
        package: {},
      },
    };
  },
  methods: {
    onNextHandler(e) {
      if (e) {
        this.formData = { ...e };
      }
      this.step += 1;
    },
  },
};
</script>
<style>
 .wizard-container {
   @apply bg-gray-100 w-3/6 m-auto p-6 mt-12;
 }
 h1 {
   @apply text-black font-bold text-2xl;
 }
 button {
   @apply text-sm px-5 py-1
 }
 .button-black {
   @apply bg-black text-white;
 }
 .button-white {
   @apply bg-white text-black border-gray-400;
 }
</style>
