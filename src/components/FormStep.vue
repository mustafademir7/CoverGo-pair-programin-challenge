<template>
  <div>
    <template v-if="isValid">
      <h1>Tell us about yourself</h1>
      <div class="form mt-3">
      <div class="form-item">
        <div class="label">Name</div>
        <input class="input" placeholder="Name" v-model="formItems.name" />
      </div>
      <div class="form-item">
        <div class="label">Age</div>
        <input class="input" placeholder="Age" v-model.number="formItems.age" />
      </div>
      <div class="form-item">
        <div class="label">Where do you live</div>
        <select v-model="formItems.city" class="input">
          <option v-for="(c,i) in cities" :value="c" :key="i">{{ c.country }}</option>
        </select>
      </div>
      <div>
        <div>
          <div v-for="(p, pi) in packages" :key="pi">
            <label :for="'opt'+1">
              <input type="radio" :id="'opt'+ pi" name="opt" :value="p"
                     v-model="formItems.package"> <small>{{ p.name }}</small>
                     <PackageInformation :packageInfo="p"
                                         :city="formItems.city"
                                         :age="formItems.age"
                                         v-if="p.val" />

            </label>
          </div>
        </div>
      </div>
      <div class="premium-info" v-if="premium">
        Your premium is {{ premium }}
      </div>
      <div class="mt-12 text-center">
        <button class="button-white mr-2" @click="$emit('onBack')">Back</button>
        <button class="button-black ml-2" @click="onValidate">Next</button>
      </div>
    </div>
    </template>
    <div class="error" v-if="!isValid">
      <h1>Ooooops</h1>
      <div class="my-6">
        <div>Your age is over out accepted limit.</div>
        <div>We are sorry abut that we can ot insure you now.</div>
      </div>
      <button class="button-black px-9" @click="$emit('onReset')">Ok :(</button>

    </div>
  </div>
</template>

<script>
export default {
  name: 'FormStep',
  components: {
    PackageInformation: () => import('./PackageInformation.vue'),
  },
  props: {
    formData: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isValid: true,
      cities: [
        { country: 'Honkong', currency: 'HKD', rate: 1 },
        { country: 'USA', currency: 'USD', rate: 2 },
        { country: 'Austuralia', currency: 'AUD', rate: 3 },
      ],
      packages: [
        { name: 'Standart', val: 0 },
        { name: 'Safe', val: 50 },
        { name: 'Super Safe', val: 75 },
      ],
      formItems: {},
    };
  },
  computed: {
    premium() {
      const rate = this.formItems?.city.rate ?? 1;
      const age = this.formItems?.age ?? 0;
      const percent = this.formItems?.package.val ?? 0;
      let total = age * 10 * rate;
      if (percent) {
        total += (total * percent) / 100;
      }
      return total;
    },
  },
  methods: {
    onValidate() {
      if (this.formItems.age > 100) {
        this.isValid = false;
        return;
      }
      this.$emit('onNext', { ...this.formItems, premium: this.premium });
    },
  },
  created() {
    this.formItems = { ...this.formData };
  },
};
</script>

<style scoped>
  .form {
    @apply text-left mx-auto w-1/2;
  }
  .form-item {
    @apply mb-2;
  }
 .label {
   @apply text-left text-sm text-gray-400 mb-1;
 }
  .input {
   @apply w-full border-gray-400 border
 }
  .premium-info {
    @apply text-black font-bold text-base mt-12 text-center;
  }
</style>
