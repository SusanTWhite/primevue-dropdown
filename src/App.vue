<template>
  <div class="card flex justify-content-center">
    <Dropdown
      v-model="selectedCity"
      :options="cities"
      placeholder="Select a City"
      class="w-full md:w-14rem"
      v-on:change="expirationDate"
    />
  </div>
  <div class="card flex">Selected City: {{ selectedCity }}</div>
  <div class="card flex">
    Expiration:&nbsp;<Calendar v-model="decisionExpirationDate" />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const selectedCity = ref('');
/*
const cities = ref([
  { name: 'New York', code: 'NY' },
  { name: 'Rome', code: 'RM' },
  { name: 'London', code: 'LDN' },
  { name: 'Istanbul', code: 'IST' },
  { name: 'Paris', code: 'PRS' },
]);
*/
const cities = ref(['New York', 'Rome', 'London', 'Istanbul', 'Paris']);
const later = new Date('2025-12-17T03:24:00');
const defaultDate = new Date('2023-12-31T00:00:00')
const now = new Date();
const decisionExpirationDate = ref(defaultDate);

//Accept override value if present, calculate if not
const expirationDate = () => {
  const input = selectedCity.value;
  console.log('Selected: ' + input);
  if (input == 'London') {
    decisionExpirationDate.value = now;
    //alert(decisionExpirationDate.value);
  } else {
    decisionExpirationDate.value = later;
    //alert(decisionExpirationDate.value);
  }
  if (decisionExpirationDate.value != undefined) {
    return decisionExpirationDate.value;
  } else {
    return 'No Date';
  }
};

</script>
